# <font color=red>MQ</font>

- [<font color=red>MQ</font>](#font-colorredmqfont)
  - [MQ 作用](#mq-作用)
  - [MQ 的缺点](#mq-的缺点)
  - [<font color=blue>Kafka</font>](#font-colorbluekafkafont)
      - [名词概念解释](#名词概念解释)
      - [高可用原理](#高可用原理)
      - [高吞吐量原理](#高吞吐量原理)
      - [消息格式](#消息格式)
      - [为什么 Kafka 分区数变多后性能降低](#为什么-kafka-分区数变多后性能降低)
  - [<font color=blue>RabbitMQ</font>](#font-colorbluerabbitmqfont)
      - [AMQP 协议](#amqp-协议)
      - [名词概念解释](#名词概念解释-1)
      - [高可用原理](#高可用原理-1)
      - [事务消息](#事务消息)
  - [<font color=blue>RocketMQ</font>](#font-colorbluerocketmqfont)
      - [名词概念解释](#名词概念解释-2)
      - [高可用原理](#高可用原理-2)
      - [存储结构](#存储结构)
      - [Pull 模式、Push 模式](#pull-模式push-模式)
      - [延迟消息](#延迟消息)
      - [顺序消息](#顺序消息)
      - [事务消息](#事务消息-1)
      - [消费回溯](#消费回溯)
  - [<font color=blue>Kafka、ActiveMQ、RabbitMQ、RocketMQ 的优缺点</font>](#font-colorbluekafkaactivemqrabbitmqrocketmq-的优缺点font)

## MQ 作用

1. 解耦
2. 异步
3. 削峰

## MQ 的缺点

1. 系统可用性降低（多了一个 MQ 服务）
2. 系统复杂度提高（消息丢失、消息重复等问题需要处理）
3. 数据一致性问题（无法确保多个系统之间的数据一致性）

## <font color=blue>Kafka</font>

#### 名词概念解释

- Broker：消息中间件节点，一个节点就是一个 broker，一个或者多个 Broker 可以组成一个集群
- Topic：主题，Kafka 根据 topic 对消息进行归类，发布到 Kafka 集群的每条消息都需要指定一个 topic
- Producer：消息生产者，向 Broker 发送消息的客户端
- Consumer：消息消费者，从 Broker 读取消息的客户端
- ConsumerGroup：每个 Consumer 属于一个特定的 Consumer Group，一条消息可以被多个不同的 Consumer Group 消费，一条消息只能被 Consumer Group 中的一个 Consumer 消费
- Partition：分区，一个 topic 可以分为多个 partition，每个 partition 内部的消息是有序的
- Segment：分段，一个 Partition 划分为多个 segment file（一个数据文件+一个索引文件），Parition 是文件夹
- Replica：副本，每个 Topic 可以设置有 N 个副本（replica），副本数最好要小于 broker 的数量，每个 Topic 的多个 replica 分为 Lerder replica 和 follower replica
- ISR（in-sync replica）：
  - 副本同步集合，每个分区都有自己的一个 ISR 集合
  - 处于 ISR 集合中的副本，意味着 follower 副本与 leader 副本保持同步状态
  - 只有处于 ISR 集合中的副本才有资格被选举为 leader
  - ISR 由 leader 维护，如果有 follower 副本没有响应或消息延时太大，那么 leader 会将该 follower 副本移除
  - 判断 follower 副本可移除的条件：
    - 没有响应，由参数 replica.log.time.max.ms 决定
    - 消息延时
      - 0.9.0.0 版本之前：由参数 replica.log.max.messages 决定，即允许 follower 副本落后 leader 副本的消息数量，超过这个数量后，follower 会被踢出 ISR
      - 0.9.0.0 版本之后，由参数 replica.lag.time.max.ms 决定，该参数指的是允许 follower 副本不同步消息的最大时间值，即只要在 replica.lag.time.max.ms 时间内 follower 有同步消息，即认为该 follower 处于 ISR 中

#### 高可用原理

- Kafka 0.8 以后，提供了 HA 机制，就是 replica（复制品） 副本机制
- 每个 partition 的数据都会同步到其它机器上，形成自己的多个 replica 副本。所有 replica 会选举一个 leader 出来，生产和消费都跟这个 leader 交互，然后其他 replica 就是 follower。写的时候，leader 会负责把数据同步到所有 follower 上去（可配置 ack 机制），读的时候就直接读 leader 上的数据即可
- 写数据的时候，生产者就写 leader，然后 leader 将数据落地写本地磁盘，接着其他 follower 自己主动从 leader 来 pull 数据，可以根据配置返回 ack 给 leader
- 消费的时候，只会从 leader 去读
- **判断节点存活的方法：**
  1. broker 必须维护和 zookeeper 的连接，zookeeper 会通过心跳机制检查每个节点的连接
  2. follower 必要能及时同步与 leader 的写操作，不能延时太久

#### 高吞吐量原理

- 顺序读写
  - kafka 的消息是不断追加到文件中的，这个特性使 kafka 可以充分利用磁盘的顺序读写性能
  - 顺序读写不需要硬盘磁头的寻道时间，只需很少的扇区旋转时间，所以速度远快于随机读写
  - 一般而言要高出磁盘随机读写三个数量级，一些情况下磁盘顺序读写性能甚至要高于内存随机读写
- Page Cache
  - 为了优化读写性能，Kafka 利用了操作系统本身的 Page Cache，就是利用操作系统自身的内存而不是 JVM 空间内存
- 零拷贝
  - Kafka 采用的是 sendfile 零拷贝方式，允许操作系统将数据从 Page Cache 直接发送到网络，只需要最后一步的 copy 操作将数据复制到 NIC 缓冲区， 这样避免重新复制数据
- 分区、分段（Partition、Segment）
  - 每个 Topic 分为多个 Partition，每个 Partition 又分为多个 Segment，所以每次操作都是针对一小部分做操作，很轻便，并且增加并发能力强
- 批量发送
  - kafka 允许进行批量发送消息，producter 发送消息的时候，可以将消息缓存在本地,等到了固定条件发送到 kafka
  - 批量发送的阈值条件：
    - 积压的消息条数阈值
    - 发送的时间间隔阈值
- 数据压缩
  - Kafka 使用了批量压缩，即将多个消息一起压缩而不是单个消息压缩
  - Kafka 允许使用递归的消息集合，批量的消息可以通过压缩的形式传输并且在日志中也可以保持压缩格式，直到被消费者解压缩
  - Kafka 支持多种压缩协议，包括 Gzip 和 Snappy 压缩协议
  - 数据压缩需要和批量发送一起使用，单条做数据压缩的话，压缩率相对很低，效果不明显

#### 消息格式

- 消息由一个固定长度的头部和可变长度的字节数组组成。头部包含了一个版本号和 CRC32 校验码
  1. 消息长度: 4 bytes (value: 1+4+n)
  2. 版本号: 1 byte
  3. CRC 校验码: 4 bytes
  4. 具体的消息: n bytes

#### 为什么 Kafka 分区数变多后性能降低

- 同时开启的文件句柄数高：分区越多，在底层操作系统中配置打开文件句柄限制所需要的分区就越高
- 副本复制代价大：分区太多，一旦 Broker 宕机，重新选举每个 Topic 的 leader 副本的时间会变长，从 ZooKeeper 初始化元数据每个分区的时间也会很长
- 增加端到端延迟：发送消息后，leader 副本的消息复制到 follower 副本的时间会增长，消息发送的延迟就会增高
- 客户端需要更多内存存储分区信息：客户端发送消息需要分区信息，因此分区越多，内存占用越大

## <font color=blue>RabbitMQ</font>

#### AMQP 协议

- AMQP（Advanced Message Queuing Protocol）是一个提供统消息服务的应用层标准高级消息队列协议，是应用层协议的一个开放标准，为面向消息的中间件设计
- AMQP 模型包括一套用于路由和存储消息的功能模块，以及一套在这些模块之间交换消息的规则
- AMQP 模型描述了一套模块化的组件以及这些组件之间进行连接的标准规则
  - exchange：接收发布应用程序发送的消息，并根据一定的规则将这些消息路由到“消息队列”
  - message queue：存储消息，直到这些消息被消费者安全处理完为止
  - binding：定义了 exchange 和 message queue 之间的关联，提供路由规则

#### 名词概念解释

- Broker: 消息中间件节点，一个节点就是一个 broker，一个或者多个 Broker 可以组成一个集群
- Virtual host: 出于多租户和安全因素设计的，把 AMQP 的基本组件划分到一个虚拟的分组中，类似于网络中的 namespace 概念。当多个不同的用户使用同一个 RabbitMQ server 提供的服务时，可以划分出多个 vhost，每个用户在自己的 vhost 创建 exchange／queue 等
- ConnectionFactory：连接管理器
- Connection: publisher／consumer 和 broker 之间的 TCP 连接。断开连接的操作只会在 client 端进行，Broker 不会断开连接，除非出现网络故障或 broker 服务出现问题
- Channel：Channel 是在 connection 内部建立的逻辑连接，是轻量级的 Connection
- Exchange: 路由器，message 到达 Broker 的第一站，根据分发规则，匹配查询表中的 routing key，分发消息到 queue 中去
  - Exchange 类型：
  - DirectExchange (point-to-point)：通过一个 routingKey 与 Queue 一对一绑定
  - TopicExchange (publish-subscribe) ：可以通过特定格式的 routingKey 匹配规则，支持 Exchange 与 Queue 一对多绑定（\*代表过滤一个单词，#代表过滤后面所有单词，多个单词用.隔开）
  - FanoutExchange (multicast)：类似广播模式，只要与他绑定了的 Queue， 他就会把消息发送给对应 Queue（与 routingKey 没关系）
- Queue: 队列，消息最终被送到这里等待 consumer 取走。一个 message 可以被同时拷贝到多个 queue 中
- RoutingKey：路由键，用于把生成者的数据分配到交换器上
- BindingKey: 绑定键，Exchange 和 Queue 之间的虚拟连接，binding 中可以包含 routing key。Binding 信息被保存到 exchange 中的查询表中，用于 message 的分发依据

#### 高可用原理

- RabbitMQ 是基于主从（非分布式）做高可用性的
- RabbitMQ 集群模式有三种：单机模式、普通集群模式、镜像集群模式
  - 普通集群模式（无高可用性）
    - 在多台机器上启动多个 RabbitMQ 实例
    - 新建的 queue，只会放在一个 RabbitMQ 实例上，但是其他的每个实例都会同步 queue 的元数据（元数据可以认为是 queue 的一些配置信息，通过元数据，可以找到 queue 所在实例）。
    - 消费的时候，如果连接到了另外一个实例，那么那个实例会从 queue 所在实例上拉取数据过来
    - 没有高可用性，主要为了提高吞吐量
  - 镜像集群模式（高可用性）
    - 在多台机器上启动多个 RabbitMQ 实例
    - 新建的 queue，无论元数据还是 queue 里的消息都会存在于多个实例上，每个 RabbitMQ 节点都有这个 queue 的一个完整镜像，包含 queue 的全部数据，写消息到 queue 的时候，会自动把消息同步到其他的多个实例的 queue 上
    - 能保证高可用，但是性能开销大，无法线性扩展，单节点的容量上限决定了集群的容量上限

#### 事务消息

- RabbitMQ 为我们提供了两种事务消息的实现方式
  - 事务机制
    - RabbitMQ 中与事务机制有关的方法有三个：txSelect(), txCommit()以及 txRollback()
    - txSelect 用于将当前 channel 设置成 transaction 模式
    - txCommit 用于提交事务
    - txRollback 用于回滚事务
    - 在通过 txSelect 开启事务之后，我们便可以发布消息给 broker 代理服务器了，如果 txCommit 提交成功了，则消息一定到达了 broker 了，如果在 txCommit 执行之前 broker 异常崩溃或者由于其他原因抛出异常，这时候我们便可以捕获异常通过 txRollback 回滚事务
    - 缺点：会阻塞消息发送，严重影响性能
  - Confirm 模式
    - 生产者将信道设置成 confirm 模式，一旦信道进入 confirm 模式，所有在该信道上面发布的消息都会被指派一个唯一的 ID(从 1 开始)
    - 一旦消息被投递到所有匹配的队列之后，broker 就会发送一个确认给生产者（包含消息的唯一 ID）
    - confirm 模式最大的好处在于他是异步的，一旦发布一条消息，生产者应用程序就可以在等信道返回确认的同时继续发送下一条消息
    - 缺点：无法确保消息发送成功后本地事务可以执行成功，因此不是完全的事务消息

## <font color=blue>RocketMQ</font>

#### 名词概念解释

- Broker：消息中间件节点，一个节点就是一个 broker，一个或者多个 Broker 可以组成一个集群
- NameServer：路由注册中心
  - **NameServer 之间互不通信**
  - **Broker 会与每个 NameServer 保持长连接**
  - **Producer 与 NameServer 集群中的一台服务器建立长连接**
  - **Producer 持有整个 NameServer 集群的列表**
  - Broker 每 30s 向 NameServer 发送心跳包，心跳包中包含主题的路由信息（主题的读写队列数、操作权限等），NameServer 会通过 HashMap 更新 Topic 的路由信息，并记录最后一次收到 Broker 的时间戳
  - NameServer 以每 10s 的频率清除已宕机的 Broker，NameServer 认为 Broker 宕机的依据是如果当前系统时间戳减去最后一次收到 Broker 心跳包的时间戳大于 120s
  - **Producer 以每 30s 的频率去拉取主题的路由信息，如果增加了新的 Broker 或者 Broker 宕机，Producer 并不会立即感知**
  - **当 Producer 向 Broker 发送消息返回异常后，Producer 会在接下来一定时间内不会再次选择该 Broker 上的队列（时间可配置）**
- Topic：主题，RocketMQ 根据 topic 对消息进行归类，发布到 RocketMQ 集群的每条消息都需要指定一个 topic
- Queue：Topic 和 Queue 是 1 对多的关系，一个 Topic 下可以包含多个 Queue，主要用于负载均衡。**发送消息时，用户只指定 Topic，Producer 会根据 Topic 的路由信息选择具体发到哪个 Queue 上。Consumer 订阅消息时，会根据负载均衡策略决定订阅哪些 Queue 的消息**
- Producer：消息生产者，向 Broker 发送消息的客户端
- Producer Group：生产者组，多个发送同一类消息的 Producer 称为一个生产者组，**作用是在一个 Producer 宕机之后，本地事务回滚后，可以继续联系该组下的另外一个生产者实例，避免影响业务**
- Consumer：消息消费者，从 Broker 读取消息的客户端
- Consumer Group：消费者组，消费同一类消息的多个 Consumer 实例组成一个消费者组，一个 Consumer Group 下的多个 Consumer 以均摊方式消费消息，如果设置为广播方式，那么这个 Consumer Group 下的每个实例都消费全量数据

#### 高可用原理

- RocketMQ 每个 Topic 的多个 Queue 会分散在多个 Broker 上，每个 Queue 持有一部分数据，且支持给 Master 节点设置 Slave 节点
- NameServer 一般是集群化部署，每个 NameServer 会互相同步收到的元数据，保证各个 NameServer 上包含的集群元数据都是相同的，一旦 Broker 宕机，会通知对应的 Slave 切换为 Master 保证高可用
- RocketMQ 默认支持三种集群模式
  - 双 Master : 优点是配置简单、快捷，但是一旦 MASTER 机器宕机或出现问题就无法提供服务
  - 双 Master 双 Slave 同步双写： 比异步复制的性能差 10%，但能保证数据不丢失
  - 双 Master 双 Slave 异步复制：性能最好，但是遇到突发情况会有少量数据丢失（Master 宕机，未同步到 Slave 节点的数据将会丢失）

#### 存储结构

- RocketMQ 存储设计主要包含 CommitLog 文件、ConsumeQueue 文件和 IndexFile 文件
- CommitLog 文件
  - 消息存储文件，所有 Topic 的消息随着到达 Broker 的顺序写入 CommitLog 文件，每个文件默认为 1G，文件的命名也及其巧妙，使用该存储在消息文件中的第一个全局偏移量来命名文件，该文件使用顺序写
- ConsumeQueue 文件
  - 消息消费队列文件，是 CommitLog 文件的基于 Topic 的索引文件，主要用于消费者根据 Topic 消费消息，其组织方式为 /topic/queue，同一个队列中存在多个文件，ConsumeQueue 设计极具技巧性，其每个条目使用固定长度（8 字节 CommitLog 物理偏移量、4 字节消息长度、8 字节 Tag HashCode），这里不是存储 tag 的原始字符串，而是存储 HashCode，目的就是确保每个条目的长度固定，可以使用访问类似数组下标的方式来快速定位条目，极大的提高了 ConsumeQueue 文件的读取性能
- IndexFile 文件
  - 基于物理磁盘文件实现 Hash 索引。其文件由 40 字节的文件头、500W 个 Hash 槽，每个 Hash 槽为 4 个字节，最后由 2000 万个 Index 条目，每个条目由 20 个字节构成，分别为 4 字节的索引 key 的 HashCode、8 字节消息物理偏移量、4 字节时间戳、4 字节的前一个 Index 条目( Hash 冲突的链表结构)

#### Pull 模式、Push 模式

- Pull 模式
  - Consumer 遍历 Queue 集合，批量获取每个 Queue 的消息，并记录 offset
  - 消费者从 server 端拉消息，主动权在消费端，可控性好，但需要控制消费速度，否则会造成大量空 pull 请求（消费间隔时间太短）或者消息处理不及时（消费间隔时间太长）
- Push 模式
  - PullMessageService 轮询拉取消息，通过 Consumer 注册的 MessageListener 监听器将消息传到 Consumer 中，对用户而言，感觉消息是被推送过来的
  - 缺点：Push 模式速度过快，如果消息处理很慢，会导致内存中堆积的消息增多，为此 RocketMQ 还实现了消费端的限流（根据消息堆积数量和消息堆积大小决定是否控制消费速度）

#### 延迟消息

- RocketMQ 支持延时消息，但是不支持任意时间精度，支持特定的 level，例如定时 5s，10s，1m 等
- **所有的延迟消息由 producer 发出之后，都会存放到同一个 topic（SCHEDULE_TOPIC_XXXX）下，不同的延迟级别会对应不同的队列序号**
- **当延迟时间到之后，由定时线程读取转换为普通的消息存的真实指定的 topic 下，此时对于 consumer 端此消息才可见，从而被 consumer 消费**

#### 顺序消息

- RocketMQ 提供了两种顺序消息级别
  - 普通顺序消息：**Producer 使用同步的方式发送消息，重写 MessageQueueSelector()接口，实现消息按照严格的顺序存储在 rocketmq 的一个相同的 queue 里面**
  - 完全严格顺序 ：在 普通顺序消息 的基础上，Consumer 严格顺序消费，**采用分布式锁，确保同时只有一个 Consumer 在消费消息，每次 OrderlyQueue 变更 Consumer 时必须确保消息全部被消费完了，才可以释放锁**

#### 事务消息

- RocketMQ 提供了事务消息的功能，采用 2PC(两段式协议)+补偿机制（事务回查）的分布式事务功能
  - 事务消息发送步骤：
    1. Producer 将半事务消息（Half）发送至 Broker
    2. Broker 将消息持久化成功之后，向 Producer 返回 ack 确认消息已经发送成功，此时消息为半事务消息
    3. Producer 开始执行本地事务
    4. Producer 根据本地事务执行结果向 Broker 提交二次确认（Commit 或是 Rollback）
    5. 如果 Broker 收到 Commit 状态，则将半事务消息标记为可投递，使 Consumer 对该消息可见
    6. 如果 Broker 收到 Rollback 状态，则删除半事务消息，Consumer 将不会消费到该消息
    7. 如果 Broker 未收到了确认消息，Broker 会定时回查本地事务的执行结果，以确保查到最终的事务结果
- 消息回查：Broker 通过扫描发现某条消息长期处于“半事务消息”状态时，需要主动向 Producer 询问该消息的最终状态（Commit 或是 Rollback），如果 Producer 返回的状态是 Unknown，则表示本地事务结果无法确认，Broker 会继回查，知道成功或者失败

#### 消费回溯

- Broker 在向 Consumer 投递成功消息后，可以配置消息保留时长，消息仍然会保留
- RocketMQ 支持按照时间回溯消费，时间维度精确到毫秒，可以向前回溯，也可以向后回溯

## <font color=blue>Kafka、ActiveMQ、RabbitMQ、RocketMQ 的优缺点</font>

| 特性                     | ActiveMQ                              | RabbitMQ                                           | RocketMQ                                                                                                              | Kafka                                                                                                                                           |
| ------------------------ | ------------------------------------- | -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| 单机吞吐量               | 万级，比 RocketMQ、Kafka 低一个数量级 | 同 ActiveMQ                                        | 10 万级，支撑高吞吐                                                                                                   | 10 万级，高吞吐，一般配合大数据类的系统来进行实时数据计算、日志采集等场景                                                                       |
| topic 数量对吞吐量的影响 |                                       |                                                    | topic 可以达到几百/几千的级别，吞吐量会有较小幅度的下降，这是 RocketMQ 的一大优势，在同等机器下，可以支撑大量的 topic | topic 从几十到几百个时候，吞吐量会大幅度下降，在同等机器下，Kafka 尽量保证 topic 数量不要过多，如果要支撑大规模的 topic，需要增加更多的机器资源 |
| 时效性                   | ms 级                                 | 微秒级，这是 RabbitMQ 的一大特点，延迟最低         | ms 级                                                                                                                 | 延迟在 ms 级以内                                                                                                                                |
| 可用性                   | 高，基于主从架构实现高可用            | 同 ActiveMQ                                        | 非常高，分布式架构                                                                                                    | 非常高，分布式，一个数据多个副本，少数机器宕机，不会丢失数据，不会导致不可用                                                                    |
| 消息可靠性               | 有较低的概率丢失数据                  | 基本不丢                                           | 经过参数优化配置，可以做到 0 丢失                                                                                     | 同 RocketMQ                                                                                                                                     |
| 功能支持                 | MQ 领域的功能极其完备                 | 基于 erlang 开发，并发能力很强，性能极好，延时很低 | MQ 功能较为完善，还是分布式的，扩展性好                                                                               | 功能较为简单，主要支持简单的 MQ 功能，在大数据领域的实时计算以及日志采集被大规模使用                                                            |

- ActiveMQ 没经过大规模吞吐量场景的验证，社区也不是很活跃
- RabbitMQ 基于 erlang 开发，不易维护，但开源社区最活跃
- RocketMQ 由阿里开源，已经捐献给 Apache 成为顶级项目，开源社区活跃度一般
- Kafka 在大数据领域是业内标准，开源社区活跃度很高
