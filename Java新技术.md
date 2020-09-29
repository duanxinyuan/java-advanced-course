# <font color=red>JAVA 新技术</font>

[toc]

## <font color=blue>响应式编程</font>

- 简介
  - 响应式编程为 Java 的企业版应用提供了更高的性能，并降低了内存消耗
  - 主要是通过减少进程的上下文切换（将耗时的 IO 操作变成异步）来实现的。因为类似的上下文切换对 CPU 和内存的消耗是极大，所以要尽可能的减少这样的切换操作
  - 不过，响应式编程带来的这种性能上的提高，代价是降低了软件的维护性
- 框架：
  - Java 8 的 Stream 流，Observable 和 Observer 模式
  - RxJava：移动端用的较多的框架，基于观察者模式
  - WebFlux：Flux 和 Mono，Flux 主要是针对 0-N 的元素，Mono 主要是针对 0-1 个元素
  - Reactor：类似 WebFlux
- RSocket
  - 一种二进制的点对点通信协议，是一种新的网络通信第七层（应用层）协议
  - 旨在用于分布式应用程序中，是 HTTP 等其他协议的替代方案
  - 基于 Reactive Streams 规范具有异步，多路复用，断线重连，基于消息等特性
  - 它由 Facebook，Netifi 和 Pivotal 等工程师开发，提供 Java，JavaScript，C ++和 Kotlin 等实现，Spring framework 最近的几次更新都特别对其进行了支持。知名 rpc 框架 Dubbo 从 3 开始也针对 RSocket 进行了适配
  - RSocket 定义了四种交互模型来弥补 Http 协议的不足之处：
    - Fire-and-Forget：优化请求/响应，在不需要响应时非常有用，例如非关键事件日志记录
    - Request/Response：类似 Http 的请求/响应模型 但是具有 Http 没有的优点，它是异步和多路复用的
    - Request/Stream：单个请求可以接收多个响应。例如获取视频列表、获取目录中的产品
    - Channel: 该模型模型提供双向通信。在此模型中，消息流在两个方向上异步流动。例如发生更改时，从服务器向客户端发出增量/差异

## <font color=blue>JAVA 8（LTS 版本（长期支持版本））</font>

- **函数式接口 FunctionInterface 与 Lambda 表达式**：函数式编程，允许把函数作为一个方法的参数（例：(parameters) -> expression）
- **Stream API**：新添加的 Stream API（java.util.stream） 把真正的函数式编程风格引入到 Java 中
- **接口 default 方法**: 接口里面可以直接实现方法
- **Date Time API**：加强对日期与时间的处理
- **反射增强**：可以通过反射来获取方法的参数名
- **Optional 类**：Optional 类已经成为 Java 8 类库的一部分，用来解决空指针异常
- **方法引用**：方法引用提供了非常有用的语法，可以直接引用已有 Java 类或对象（实例）的方法或构造器。与 lambda 联合使用，方法引用可以使语言的构造更紧凑简洁，减少冗余代码（例：System.out::print）
- 新工具：新的编译工具，如：Nashorn 引擎 jjs、 类依赖分析器 jdeps
- Nashorn, JavaScript 引擎 − Java 8 提供了一个新的 Nashorn javascript 引擎，它允许我们在 JVM 上运行特定的 javascript 应用
- String.join、Arrays.parallelSort、StampedLock、LongAdder、LongAccumulator 等

## <font color=blue>JAVA 9</font>（Jigsaw、JShell、Reactive Streams）

- **模块系统：模块是一个包的容器，Java 9 最大的变化之一是引入了模块系统（Jigsaw 项目）**
- **REPL (JShell)：交互式编程环境**
  - JShell 是 Java 9 新增的一个交互式的编程环境工具
  - 它允许你无需使用类或者方法包装来执行 Java 语句
  - 它与 Python 的解释器类似，可以直接 输入表达式并查看其执行结果
- **HTTP 2 客户端**：HTTP/2 标准是 HTTP 协议的最新版本，新的 HTTPClient API 支持 WebSocket 和 HTTP2 流以及服务器推送特性
- 改进的 Javadoc：Javadoc 现在支持在 API 文档中的进行搜索。另外，Javadoc 的输出现在符合兼容 HTML5 标准
- 多版本兼容 JAR 包：多版本兼容 JAR 功能能让你创建仅在特定版本的 Java 环境中运行库程序时选择使用的 class 版本
- 集合工厂方法：List，Set 和 Map 接口中，新的静态工厂方法可以创建这些集合的不可变实例
- 私有接口方法：在接口中使用 private 私有方法。我们可以使用 private 访问修饰符在接口中编写私有方法
- 进程 API：改进的 API 来控制和管理操作系统进程。引进 java.lang.ProcessHandle 及其嵌套接口 Info 来让开发者逃离时常因为要获取一个本地进程的 PID 而不得不使用本地代码的窘境
- 改进的 Stream API：改进的 Stream API 添加了一些便利的方法，使流处理更容易，并使用收集器编写复杂的查询
- **响应式流（Reactive Streams) API：Java 9 中引入了新的响应式流 API 来支持 Java 9 中的响应式编程**
- 改进 try-with-resources：如果你已经有一个资源是 final 或等效于 final 变量,您可以在 try-with-resources 语句中使用该变量，而无需在 try-with-resources 语句中声明一个新变量
- 改进的弃用注解 @Deprecated：注解 @Deprecated 可以标记 Java API 状态，可以表示被标记的 API 将会被移除，或者已经破坏
- 改进钻石操作符(Diamond Operator) ：匿名类可以使用钻石操作符(Diamond Operator)
- 改进 Optional 类：java.util.Optional 添加了很多新的有用方法，Optional 可以直接转为 stream
- 多分辨率图像 API：定义多分辨率图像 API，开发者可以很容易的操作和展示不同分辨率的图像了
- 改进的 CompletableFuture API ： CompletableFuture 类的异步机制可以在 ProcessHandle.onExit 方法退出时执行操作
- 轻量级的 JSON API：内置了一个轻量级的 JSON API

## <font color=blue>JAVA 10</font>（局部变量类型推断、G1 的并行 Full GC、ThreadLocal 握手机制）

- **var 局部变量类型推断**：引入"var"关键字，可以随意定义变量而不必指定变量的类型
- 统一 JDK 仓库：将原来用 Mercurial 管理的众多 JDK 仓库代码，合并到一个仓库中，简化开发和管理过程
- **统一垃圾回收接口**：引入一个纯净的垃圾收集器接口，以帮助改进不同垃圾收集器的源代码隔离
- **G1 的并行 Full GC**：截止到 Java 9，G1 的 Full GC 采用的是单线程算法，Java10 开始，在发生 Full GC 时可以使用多个线程进行并行回收
- **应用程序类数据 (AppCDS) 共享**：通过跨进程共享通用类元数据来减少内存占用空间，和减少启动时间
- **ThreadLocal 握手机制**：在不进入到全局 JVM 安全点 (Safepoint) 的情况下，对线程执行回调。优化可以只停止单个线程，而不是停全部线程或一个都不停
- 移除 JDK 中附带的 javah 工具。可以使用 javac -h 代替
- 使用附加的 Unicode 语言标记扩展
- 能将堆内存占用分配给用户指定的备用内存设备
- 使用 Graal 基于 Java 的编译器，可以预先把 Java 代码编译成本地代码来提升效能
- OpenJDK 中提供一组默认的根证书颁发机构证书。开源目前 Oracle 提供的的 Java SE 的根证书，这样 OpenJDK 对开发人员使用起来更方便

## <font color=blue>JAVA 11（LTS 版本（长期支持版本））</font>（ZGC、Epsilon、增强 var）

- **用于 Lambda 参数的局部变量语法**：可以在 Lambda 表达式中使用 var，提高代码可读性（例如：(var x, var y) -> x.process(y)）
- **ZGC**
  - ZGC 即 Z Garbage Collector，处于实验性阶段，只在 Linux/x64 上可用
  - ZGC 是一个可伸缩的、低延迟的垃圾收集器
  - 主要为了满足如下目标进行设计：
    - GC 停顿时间不超过 10ms
    - 即能处理几百 MB 的小堆，也能处理几个 TB 的大堆
    - 应用吞吐能力不会下降超过 15%（与 G1 回收算法相比）
- **Epsilon 垃圾回收器**，又被称为"No-Op（无操作）"回收器
  - Epsilon 垃圾回收器的目标是开发一个控制内存分配，但是不执行任何实际的垃圾回收工作
  - 它提供一个完全消极的 GC 实现，分配有限的内存资源，最大限度的降低内存占用和内存吞吐延迟时间
  - 主要使用场景；
    - 性能测试
    - 内存压力测试
    - VM 接口测试
    - 延迟和吞吐量改进
- 低开销的堆分配采样方法：Java 11 中提供一种低开销的 Java 堆分配采样方法，能够得到堆分配的 Java 对象信息，并且能够通过 JVMTI 访问堆信息
- **支持 TLS 1.3**
- **标准 HTTP Client 升级**
  - 提供了对 HTTP/2 等业界前沿标准的支持，同时也向下兼容 HTTP/1.1
  - 精简而又友好的 API 接口，与主流开源 API（如：Apache HttpClient、Jetty、OkHttp 等）类似甚至拥有更高的性能
  - 它是 Java 在 Reactive-Stream 方面的第一个生产实践
- 基于嵌套的访问控制
- 动态的类文件常量
- 改进 Aarch64 Intrinsics
- 移除 Java EE 和 CORBA 模块，JavaFX 也已被移除
- 采用 Curve25519 和 Curve448 算法实现的密钥协议
- 实现 ChaCha20 和 Poly1305 加密算法
- 弃用 Java 8 的 Nashorn JavaScript 引擎

## <font color=blue>JAVA 12</font>（Switch 表达式）

- **Switch 表达式**
  ```java
  switch (day) {
      case MONDAY, FRIDAY, SUNDAY -> System.out.println(6);
      case TUESDAY                -> System.out.println(7);
      case THURSDAY, SATURDAY     -> System.out.println(8);
      case WEDNESDAY              -> System.out.println(9);
  }
  ```
- Shenandoah GC
  - 是 Redhat 主导开发的 Pauseless GC 实现
  - 主要目标是 99.9% 的暂停小于 10ms，以及可以处理大堆和小堆
  - 是一个实验性功能，不包含在默认（Oracle）的 OpenJDK 版本中

## <font color=blue>JAVA 13</font>（Text Blocks、Dynamic CDS Archives）

- 动态应用程序类-数据共享（Dynamic CDS Archives）
  - Java 13 中对 Java 10 中引入的 应用程序类数据共享进行了进一步的简化、改进和扩展
  - 允许在 Java 应用程序执行结束时动态进行类归档
  - 具体能够被归档的类包括：所有已被加载，但不属于默认基层 CDS 的应用程序类和引用类库中的类
  - 通过这种改进，可以提高应用程序类-数据使用上的简易性，减少在使用类-数据存档中需要为应用程序创建类加载列表的必要，简化使用类-数据共享的步骤，以便更简单、便捷地使用 CDS 存档
- 增强 ZGC 释放未使用内存：Java 13 中对 ZGC 的改进，主要体现在下面几点：
  - 释放未使用内存给操作系统
  - 释放未使用内存给操作系统
  - 添加参数：-XX:SoftMaxHeapSize 来软限制堆大小
- Socket API 重构
  - Java 13 为 Socket API 带来了新的底层实现方法，并且在 Java 13 中是默认使用新的 Socket 实现，使其易于发现并在排除问题同时增加可维护性
- Switch 表达式扩展（预览功能）
  - Java 13 中，value break 语句不再被编译，而是用 yield 来进行值返回
  ```java
  switch (number) {
      case 1, 2:
          yield "one or two";
      case 3:
          yield "three";
      case 4, 5, 6:
          yield "four or five or six";
      default:
          yield "unknown";
  };
  ```
- 文本块（Text Blocks，预览功能）
  - 13 之前的写法：
  ```java
  String json ="{\n" +
            "   \"name\":\"mkyong\",\n" +
            "   \"age\":38\n" +
            "}\n";
  ```
  - 13 之后的写法：
  ```java
  String json = """
              {
                  "name":"mkyong",
                  "age":38
              }
              """;
  ```

## <font color=blue>JAVA 14</font>（Java 打包工具、NullPointerException、record 类型）

- **优化 instanceof 的模式匹配**
  ```java
  void patternMatching(Object obj) {
    if (obj instanceof String str) {
      System.out.println(str.length());
    }
  }
  ```
- **Java 打包工具（孵化项目）**
  - 使用 jpackage 命令打包，可以将 jar 文件打包成 exe、rpm、dmg 格式的可执行文件
- **G1 GC 支持 NUMA**
  - 优化了 G1 在使用 NUMA（non-uniform memory access）时的内存分配
- **更有价值的 NullPointerException**
  - JAVA 14 增强了对 NullPointerException 异常的处理，可以显示详细的信息，错误消息可以明确的指出为空的对象
  - 这个功能需要通过选项-XX:+ShowCodeDetailsInExceptionMessages 启用
- **记录类型（Record Type，预览功能）**

  - 记录类型的作用类似于 Kotlin 中的数据类（data class)和 Scala 中的 case class

  ```java
  public class Test {

    record Pair(Object first, Object second) {}

    public static void main(String[] args) {
      Pair pair = new Pair("Hello", "World");
      System.out.println(pair.first());
      System.out.println(pair.second());
    }

  }
  ```

- **正式引入 JDK 12 的 Switch 表达式**
- **正式引入 JDK 13 的 Text Blocks（文本框）功能**
- **ZGC 的 macOS 支持和 Windows 支持**
- 新增外部内存地址访 API（MemorySegment、MemoryAddress 和 MemoryLayout）
- 新增指向 NVM（non-volatile memory，非易失性内存）的 MappedByteBuffer
- 新增 JRF（Java Flight Recorder）事件流
- **删除 CMS 垃圾回收器**
  - Concurrent Mark Sweep（CMS）垃圾回收器在 JDK 9 中被声明为废弃的。在 JDK 14 中，CMS 被移除
- 废弃 ParallelScavenge + SerialOld 的 GC 组合
