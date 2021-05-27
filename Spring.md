# <font color=red>Spring</font>
<!-- TOC -->

- [<font color=red>Spring</font>](#font-colorredspringfont)
    - [<font color=blue>SpringMVC</font>](#font-colorbluespringmvcfont)
        - [SpringMVC 组件说明](#springmvc-%E7%BB%84%E4%BB%B6%E8%AF%B4%E6%98%8E)
        - [SpringMVC 工作流程](#springmvc-%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%A8%8B)
    - [<font color=blue>SpringBoot</font>](#font-colorbluespringbootfont)
        - [SpringBoot 启动流程](#springboot-%E5%90%AF%E5%8A%A8%E6%B5%81%E7%A8%8B)
        - [Spring 常用注解](#spring-%E5%B8%B8%E7%94%A8%E6%B3%A8%E8%A7%A3)
        - [Spring 中 Bean 的作用域与生命周期](#spring-%E4%B8%AD-bean-%E7%9A%84%E4%BD%9C%E7%94%A8%E5%9F%9F%E4%B8%8E%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)
            - [Bean 的作用域](#bean-%E7%9A%84%E4%BD%9C%E7%94%A8%E5%9F%9F)
            - [Bean 的生命周期](#bean-%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)
        - [Spring IOC（Inversion of Control）原理](#spring-iocinversion-of-control%E5%8E%9F%E7%90%86)
        - [Spring IOC 容器的初始化过程](#spring-ioc-%E5%AE%B9%E5%99%A8%E7%9A%84%E5%88%9D%E5%A7%8B%E5%8C%96%E8%BF%87%E7%A8%8B)
        - [Spring AOP（Aspect Orient Programming）原理及应用场景](#spring-aopaspect-orient-programming%E5%8E%9F%E7%90%86%E5%8F%8A%E5%BA%94%E7%94%A8%E5%9C%BA%E6%99%AF)
        - [Spring AOP 和 AspectJ AOP 的区别](#spring-aop-%E5%92%8C-aspectj-aop-%E7%9A%84%E5%8C%BA%E5%88%AB)
        - [Spring 中如何将接口注册成 Bean](#spring-%E4%B8%AD%E5%A6%82%E4%BD%95%E5%B0%86%E6%8E%A5%E5%8F%A3%E6%B3%A8%E5%86%8C%E6%88%90-bean)
        - [BeanFactory 和 ApplicationContext 有什么区别？](#beanfactory-%E5%92%8C-applicationcontext-%E6%9C%89%E4%BB%80%E4%B9%88%E5%8C%BA%E5%88%AB)
        - [构造方法注入和 set 注入有什么区别？](#%E6%9E%84%E9%80%A0%E6%96%B9%E6%B3%95%E6%B3%A8%E5%85%A5%E5%92%8C-set-%E6%B3%A8%E5%85%A5%E6%9C%89%E4%BB%80%E4%B9%88%E5%8C%BA%E5%88%AB)
        - [SpringBoot 相对于 Spring 做了哪些改进？](#springboot-%E7%9B%B8%E5%AF%B9%E4%BA%8E-spring-%E5%81%9A%E4%BA%86%E5%93%AA%E4%BA%9B%E6%94%B9%E8%BF%9B)
        - [Spring 5 比 Spring4 做了哪些改进？](#spring-5-%E6%AF%94-spring4-%E5%81%9A%E4%BA%86%E5%93%AA%E4%BA%9B%E6%94%B9%E8%BF%9B)
        - [Spring 事务原理、隔离级别、传递机制](#spring-%E4%BA%8B%E5%8A%A1%E5%8E%9F%E7%90%86%E9%9A%94%E7%A6%BB%E7%BA%A7%E5%88%AB%E4%BC%A0%E9%80%92%E6%9C%BA%E5%88%B6)
        - [Spring Batch（任务批处理）](#spring-batch%E4%BB%BB%E5%8A%A1%E6%89%B9%E5%A4%84%E7%90%86)
    - [<font color=blue>SpringCloud</font>](#font-colorbluespringcloudfont)
        - [Config 配置中心](#config-%E9%85%8D%E7%BD%AE%E4%B8%AD%E5%BF%83)
        - [Bus 事件总线](#bus-%E4%BA%8B%E4%BB%B6%E6%80%BB%E7%BA%BF)
        - [Eureka 服务注册与发现](#eureka-%E6%9C%8D%E5%8A%A1%E6%B3%A8%E5%86%8C%E4%B8%8E%E5%8F%91%E7%8E%B0)
        - [Consul、Zookeeper 服务注册与发现](#consulzookeeper-%E6%9C%8D%E5%8A%A1%E6%B3%A8%E5%86%8C%E4%B8%8E%E5%8F%91%E7%8E%B0)
        - [Feign 网络远程调用](#feign-%E7%BD%91%E7%BB%9C%E8%BF%9C%E7%A8%8B%E8%B0%83%E7%94%A8)
        - [Zuul、Gateway 网关](#zuulgateway-%E7%BD%91%E5%85%B3)
        - [Ribbon 负载均衡](#ribbon-%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1)
        - [Hystrix（缓存、流控、熔断、降级、统计、监控、告警）](#hystrix%E7%BC%93%E5%AD%98%E6%B5%81%E6%8E%A7%E7%86%94%E6%96%AD%E9%99%8D%E7%BA%A7%E7%BB%9F%E8%AE%A1%E7%9B%91%E6%8E%A7%E5%91%8A%E8%AD%A6)
            - [Hystrix 线程机制实现资源控制Thread](#hystrix-%E7%BA%BF%E7%A8%8B%E6%9C%BA%E5%88%B6%E5%AE%9E%E7%8E%B0%E8%B5%84%E6%BA%90%E6%8E%A7%E5%88%B6thread)
            - [Hystrix 信号量机制实现资源控制Semaphore](#hystrix-%E4%BF%A1%E5%8F%B7%E9%87%8F%E6%9C%BA%E5%88%B6%E5%AE%9E%E7%8E%B0%E8%B5%84%E6%BA%90%E6%8E%A7%E5%88%B6semaphore)
            - [Hystrix 细粒度资源控制](#hystrix-%E7%BB%86%E7%B2%92%E5%BA%A6%E8%B5%84%E6%BA%90%E6%8E%A7%E5%88%B6)
            - [Hystrix 的 fallback（降级）机制](#hystrix-%E7%9A%84-fallback%E9%99%8D%E7%BA%A7%E6%9C%BA%E5%88%B6)
            - [Hystrix 断路器](#hystrix-%E6%96%AD%E8%B7%AF%E5%99%A8)
        - [Task 分布式任务调度](#task-%E5%88%86%E5%B8%83%E5%BC%8F%E4%BB%BB%E5%8A%A1%E8%B0%83%E5%BA%A6)
    - [<font color=blue>SpringCloud Alibaba</font>](#font-colorbluespringcloud-alibabafont)
        - [Nacos 服务注册与发现、配置中心、网络远程调用、负载均衡](#nacos-%E6%9C%8D%E5%8A%A1%E6%B3%A8%E5%86%8C%E4%B8%8E%E5%8F%91%E7%8E%B0%E9%85%8D%E7%BD%AE%E4%B8%AD%E5%BF%83%E7%BD%91%E7%BB%9C%E8%BF%9C%E7%A8%8B%E8%B0%83%E7%94%A8%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1)
        - [Sentinel 限流](#sentinel-%E9%99%90%E6%B5%81)
        - [Sentinel 和 Hystrix 的区别](#sentinel-%E5%92%8C-hystrix-%E7%9A%84%E5%8C%BA%E5%88%AB)
        - [Seata 分布式事务](#seata-%E5%88%86%E5%B8%83%E5%BC%8F%E4%BA%8B%E5%8A%A1)
        - [SchedulerX 分布式任务调度](#schedulerx-%E5%88%86%E5%B8%83%E5%BC%8F%E4%BB%BB%E5%8A%A1%E8%B0%83%E5%BA%A6)
        - [RocketMQ 消息总线](#rocketmq-%E6%B6%88%E6%81%AF%E6%80%BB%E7%BA%BF)

<!-- /TOC -->
## 1. <font color=blue>SpringMVC</font>

### 1.1. SpringMVC 组件说明

- DispatcherServlet
  - 前端控制器，也称为中央控制器
  - 它是整个请求响应的控制中心，组件的调用由它统一调度
- HandlerMapping
  - 处理器映射器，它根据用户访问的 URL 映射到对应的后端处理器 Handler
  - 也就是说它知道处理用户请求的后端处理器，但是它并不执行后端处理器，而是将处理器告诉给中央处理器
- HandlerAdapter
  - 处理器适配器，它调用后端处理器中的方法，返回逻辑视图 ModelAndView 对象
- ViewResolver
  - 视图解析器，将 ModelAndView 逻辑视图解析为具体的视图（如 JSP）
- Handler
  - 后端处理器，对用户具体请求进行处理，也就是我们编写的 Controller 类

### 1.2. SpringMVC 工作流程

1. 用户向服务端发送一次请求，这个请求会先到前端控制器 DispatcherServlet(也叫中央控制器)
2. DispatcherServlet 接收到请求后会调用 HandlerMapping 处理器映射器。由此得知，该请求该由哪个 Controller 来处理（并未调用 Controller，只是得知）
3. DispatcherServlet 调用 HandlerAdapter 处理器适配器，告诉处理器适配器应该要去执行哪个 Controller
4. HandlerAdapter 处理器适配器去执行 Controller 并得到 ModelAndView(数据和视图)，并层层返回给 DispatcherServlet
5. DispatcherServlet 将 ModelAndView 交给 ViewReslover 视图解析器解析，然后返回真正的视图
6. DispatcherServlet 将模型数据填充到视图中
7. DispatcherServlet 将结果响应给用户

## 2. <font color=blue>SpringBoot</font>

### 2.1. SpringBoot 启动流程

- 创建 SpringApplicationRunListener
- 创建参数，配置 Environment
- 创建 ApplicationContext
- 初始化 ApplicationContext，设置 Environment，加载相关 AutoConfiguration 的配置
- 刷新 ApplicationContext，常见 Bean
- 完成最终的程序启动

### 2.2. Spring 常用注解

- @EnableAutoConfiguration：SpringBoot 实现自动化配置的核心注解，通过这个注解把 spring 应用所需的 bean 注入容器中，@EnableAutoConfiguration 源码通过@Import 注入了一个 ImportSelector 的实现类
  AutoConfigurationImportSelector，这个 ImportSelector 最终实现根据我们的配置，动态加载所需的 bean
- @SpringBootConfiguration：作用与@Configuration 作用相同
- @Configuration：把一个类作为一个 IoC 容器
- @Lazy(true)：表示延迟初始化
- @Controller：用于标注控制层组件
- @Service：用于标注业务层组件
- @Component：泛指组件，当组件不好归类的时候，我们可以使用这个注解进行标注
- @Repository：用于标注数据访问组件，即 DAO 组件
- @Scope：用于指定 scope 作用域的
- @PostConstruct：用于指定初始化方法
- @PreDestory：用于指定销毁方法
- @DependsOn：定义 Bean 初始化及销毁时的顺序
- @Primary：自动装配时当出现多个 Bean 候选者时，被注解为@Primary 的 Bean 将作为首选者，否则将抛出异常
- @Autowired：Bean 注入（默认按类型注入，如果想按名称注入，可以结合@Qualifier 注解一起使用）
- @Resource：Bean 注入（默认按名称装配，当找不到与名称匹配的 bean 才会按类型装配）

### 2.3. Spring 中 Bean 的作用域与生命周期

[介绍地址 1](https://juejin.im/post/5eead904e51d4573cf6eb4e2)

[介绍地址 2](https://zhuanlan.zhihu.com/p/44875302)

#### 2.3.1. Bean 的作用域

- Spring Framework 支持五种作用域:
  - singleton
    - 单例 Bean 只在容器中存在一个实例，在 Spring 内部通过 HashMap 来维护单例 bean 的缓存，是 Spring 默认的作用域类型
  - prototype
    - 每次获取 Bean 时都会创建一个全新的 Bean
  - request
    - 每次 HTTP 请求都会创建一个全新 Bean，该 bean 仅在当前 HTTP request 内有效，该类型作用于 Web 类型的 Spring 容器
  - session
    - 每个会话创建一个全新 Bean，该类型作用于 Web 类型的 Spring 容器
  - globalSession
    - 类似于 session 作用域，只是其用于 portlet 环境的 web 应用。如果在非 portlet 环境将视为 session 作用域
    - Portlet 是基于 Java 的 Web 组件，由 Portlet 容器管理，并由容器处理请求，生产动态内容
- 作用域类型可以通过 @Scope 注解配置

#### 2.3.2. Bean 的生命周期

1. 实例化（Instantiation）
   - **使用 Java Reflection API 创建一个 Bean 的实例**
2. 属性赋值（Populate）
   - **使用 set 方法为 bean 对象设置相关属性和依赖**
3. 初始化（Initialization）
   - **如果实现了 Aware 相关接口，则执行对应接口的方法（为了让 Bean 可以获取到框架自身的一些对象，Spring 提供了一组名为\*Aware 的接口）**
     - **ApplicationContextAware: 获得 ApplicationContext 对象，**
     - BeanClassLoaderAware：获得 ClassLoader 对象，可以加载其他类到 JVM 中
     - **BeanFactoryAware：获得 BeanFactory 对象，可以调用容器的服务**
     - BeanNameAware：可以获取到 beanName
     - ApplicationEventPublisherAware：可以发布事件
     - **ResourceLoaderAware：获得 ResourceLoader 对象，可以加载外部资源**
     - ServletContextAware：获得 ServletContext 对象
     - ServletConfigAware：获得 ServletConfig 对象
   - **如果实现了 BeanPostProcessor 接口，执行 BeanPostProcessor 的 postProcessBeforeInitialization 方法（前置处理）**
   - **如果实现了 InitializingBean 接口，则调用该接口的 AfterPropertiesSet()方法，可以在 Bean 属性值设置好之后做一些操作，效果等同于自定义配置 init-method 或者使用@PostConstruct 注解**
   - **如果实现了 BeanPostProcessor 接口，执行 BeanPostProcessor 的 postProcessAfterInitialization 方法（后置处理）**
4. 销毁（Destroy）
   - **如果实现了 DisposableBean 接口的 destroy()方法，可以在 Bean 销毁之前做一些操作，效果等同于自定义配置 destory-method 或者使用@PreDestroy 注解**

### 2.4. Spring IOC（Inversion of Control）原理

- 控制反转
  - 控制：对象对于内部成员的控制
  - 反转：将之前对象管理自己内部成员，转变为 ioc 容器管理，目的是解耦
- 基本原理
  - 根据 Java 的反射机制，获取类的所有信息，再通过 xml 或者注解配置获取类与类之间的关系，最后根据以上信息构建类与类之间的依赖
- 优点：
  - 无需手动创建对象，容器会将所有 Bean 创建好，需要时去容器中取即可
  - 默认单例作用域，效率高、节省空间
  - 统一配置，方便管理

### 2.5. Spring IOC 容器的初始化过程

1. BeanDefinition 的 Resource 定位
   - 在 SpringBoot 中有三种方式实现 Resource 定位，第一个是主类所在包的，第二个是 SPI 扩展机制实现的自动装配（比如各种 starter），第三种就是@Import 注解指定的类
2. BeanDefinition 的载入
   - 使用 PathMatchingResourcePatternResolver 将扫描出来的 Resource 路径下的.class 文件都加载进来，然后遍历判断是不是有@Component/@Service 等注解，如果有的话，就是我们要装载的 BeanDefinition
3. 向 IOC 容器注册 BeanDefinition
   - 使用 BeanDefinitionRegister 注册 BeanDefinition（注入到一个 ConcurrentHashMap 中）

### 2.6. Spring AOP（Aspect Orient Programming）原理及应用场景

[介绍地址](https://blog.csdn.net/u010452388/article/details/80868392)

- Spring 中 AOP 的有两种实现方式：
  - JDK 动态代理
  - Cglib 动态代理
- 主要应用场景
  - 记录日志
  - 权限控制
  - 错误处理
  - 监控方法运行时间 （监控性能）
  - 缓存优化 （第一次调用查询数据库，将查询结果放入内存对象， 第二次调用， 直接从内存对象返回，不需要查询数据库 ）
  - 持久化
  - 事务管理 （调用方法前开启事务， 调用方法后提交关闭事务 ）

### 2.7. Spring AOP 和 AspectJ AOP 的区别

- Spring AOP
  - 基于动态代理来实现，如果使用接口实现类，默认用 JDK 提供的动态代理实现，如果是方法则使用 CGLIB 实现
  - Spring AOP 需要依赖 IOC 容器来管理，并且只能作用于 Spring 容器，使用纯 Java 代码实现
  - 在性能上，由于 Spring AOP 是基于动态代理来实现的，在容器启动时需要生成代理实例，在方法调用上也会增加栈的深度，使得 Spring AOP 的性能不如 AspectJ 的那么好
- AspectJ AOP
  - AspectJ 属于静态注入，通过在应用启动时修改代码来实现，支持编译时、编译后和加载时注入 AOP 代码
  - 可以编织字段、方法、构造函数、静态初始值设定项、最终类/方法等
  - 需要 AspectJ 编译器 (ajc)

### 2.8. Spring 中如何将接口注册成 Bean

1. 继承 ClassPathBeanDefinitionScanner，实现自定义包扫描，使用 BeanDefinitionHolder 设置 Bean 的 class 和依赖注入方式等属性
2. 实现 FactoryBean 接口，自定义 FactoryBean，可以同时实现 ApplicationContextAware、InitializingBean 等接口注入需要的容器中的对象
3. 基于 JDK 动态代理或者 Cglib 实现动态代理，让自定义 FactoryBean 的 getObject 方法返回动态代理对象
4. 最后实现 ImportBeanDefinitionRegistrar 接口，调用自定义的 ClassPathBeanDefinitionScanner 扫描包，并将自定义的 FactoryBean 注入到容器中

### 2.9. BeanFactory 和 ApplicationContext 有什么区别？

- BeanFactory 可以理解为含有 bean 集合的工厂类。BeanFactory 包含了各种 bean 的定义，以便在接收到客户端请求时将对应的 bean 实例化
- BeanFactory 还能在实例化对象的时生成协作类之间的关系。此举将 bean 自身与 bean 客户端的配置中解放出来。BeanFactory 还包含了 bean 生命周期的控制，调用客户端的初始化方法（initialization methods）和销毁方法（destruction methods）
- ApplicationContext 在 BeanFactory 基础上还提供了其他的功能：
  - 提供了支持国际化的文本消息
  - 统一的资源文件读取方式
  - 已在监听器中注册的 bean 的事件

### 2.10. 构造方法注入和 set 注入有什么区别？

- 部分依赖：假设一个类中有 3 个属性，有 3 个 arg 构造函数和 setter 方法。在这种情况下，如果您只想传递一个属性的信息，则只能通过 setter 方法
- 覆盖：Setter 注入会覆盖构造函数注入。如果我们同时使用构造函数和 setter 注入，IOC 容器将使用 setter 注入
- 在使用 set 注入时有可能还不能保证某种依赖是否已经被注入，也就是说这时对象的依赖关系有可能是不完整的

### 2.11. SpringBoot 相对于 Spring 做了哪些改进？

主要集中体现在开发、部署、测试三个方面：

1. 提供嵌入式容器支持
2. 使用命令 java -jar 独立运行 jar
3. 实现自动配置，降低了项目搭建的复杂度
4. 部署时灵活指定配置文件
5. 用于集成测试的随机端口生成

### 2.12. Spring 5 比 Spring4 做了哪些改进？

1. JDK 版本：Spring 5.0 基于 Java 8
2. 日志框架：Spring 5.0 使用自己的 spring-jcl 模块来记录日志，这个模块会自动识别并使用现有的日志框架
3. Bean 扫描机制优化：当项目非常大的时候，Spring 的扫描过程会导致很长的启动时间。在这个版本开始，你可以使用 META-INF/spring.components 文件来直接指定要注册哪些类
4. 支持 Kotlin：支持 Kotlin 函数式编程
5. 响应式编程模型：实现了 WebFlux 响应式编程模型（Mono/Flux/WebClient）
6. 单元测试优化：支持 Junit 5

### 2.13. Spring 事务原理、隔离级别、传递机制

[介绍地址](https://zhuanlan.zhihu.com/p/54067384)

- Spring 事务的底层依赖 MySQL 的事务，代码层面上利用 AOP 实现
- Spring 事务的隔离级别也依赖 MySQL 的隔离级别
- Spring 定义了七种事务传播机制
  - PROPAGATION_REQUIRED：支持当前事务，如果当前没有事务，就新建一个事务
  - PROPAGATION_SUPPORTS：支持当前事务，如果当前没有事务，就以非事务方式执行
  - PROPAGATION_MANDATORY：支持当前事务，如果当前没有事务，就抛出异常
  - PROPAGATION_NESTED：总会新建事务，如果当前有事务，则新建的事务会嵌套在当前事务内执行
    - 如果外部事务回滚，则嵌套事务也会回滚，外部事务提交的时候，嵌套事务才会被提交
    - **嵌套事务回滚不会影响外部事务**
  - PROPAGATION_REQUIRES_NEW：新建事务，如果当前存在事务，把当前事务挂起，执行当前新建事务完成以后，上下文事务恢复再执行
  - PROPAGATION_NOT_SUPPORTED：以非事务方式执行操作，如果当前存在事务，就把当前事务挂起，执行当前逻辑，结束后恢复上下文的事务
  - PROPAGATION_NEVER：以非事务方式执行，如果当前存在事务，则抛出异常
  - 常用的主要有 Required，RequiresNew，Nested 三种

### 2.14. Spring Batch（任务批处理）

## 3. <font color=blue>SpringCloud</font>

### 3.1. Config 配置中心

- 分布式配置中心
- 分为 Client（客户端）、Server（服务端）
- 缺点：
  - 配置无法自动更新，需要依赖其他工具实现配置自动同步到 client（WebHooks 或者 spring-cloud-bus）

### 3.2. Bus 事件总线

- Spring Cloud 体系内的消息总线。它可以用于广播配置文件的更改或者服务之间的通讯，也可以用于监控
- 分为 Client（客户端）、Server（服务端）
- 本质上是基于 MQ 实现消息路由，支持 RabbitMQ 和 Kafka 两种 MQ

### 3.3. Eureka 服务注册与发现

- Spring Cloud 体系内的注册中心
- 分为 Client（客户端）、Server（服务端）
- 工作流程：
  - 服务注册（Register）：把当前服务注册到注册中心，并异步向其它的 Eureka Server 节点同步服务注册信息（发送一个 POST 请求）
  - 服务续约（Renew）：Client 定期发送心跳到 Eureka Server（发送一个 PUT 请求）
  - 服务下线（Cancel）：Client 停止服务时，发送请求告知注册中心 Eureka Server 进行服务剔除下线操作（发送一个 DELETE 请求）
  - 服务剔除（Eviction）：Eureka Server 启动一个守护线程，定期（默认 90 秒）检测超时没有续约的 Client，并剔除下线

### 3.4. Consul、Zookeeper 服务注册与发现

详见微服务章节

### 3.5. Feign 网络远程调用

- Spring Cloud 体系内的 RPC 远程调用框架
- Fegin 的关键机制是使用了动态代理
- 工作流程：
  - 首先，如果你对某个接口定义了@FeignClient 注解，Feign 就会针对这个接口创建一个动态代理
  - 接着你要是调用按个接口，本质上就是调用 Feign 创建的动态代理，这是核心中的核心
  - Feign 的动态代理会根据你在接口上的@RequestMapping 等注解，来动态构造出你要请求的地址
  - 最后针对这个地址，发起 HTTP 请求，解析响应
- Fegin 是和 Ribbon 以及 Eureka 紧密协作的
  - 首先 Ribbon 会从 Eureka Client 里获取到对应的服务注册表，也就知道了所有的服务都部署在了哪些机器上，在监听哪些端口
  - 然后 Ribbon 就可以使用默认的 Round Robin 算法，从中选择一台机器
  - Fegin 就会针对这台机器，构造并发起请求

### 3.6. Zuul、Gateway 网关

- Spring Cloud 体系内的微服务网关
- 可以实现权限控制、监控、动态路由、负载均衡、限流、黑白名单过滤、静态资源处理等操作
- Zuul
  - 基于 Netflix 开源的 Zuul 实现
  - Zuul 构建于 Servlet 2.5，兼容 3.x，使用的是阻塞式的 API，不支持长连接，比如 websockets
- Gateway
  - Spring Cloud Gateway 构建于 Spring 5+，基于 Spring Boot 2.x 的 WebFlux 响应式编程模型实现
  - 非阻塞式的 API，性能上有大幅提升，支持 websockets

### 3.7. Ribbon 负载均衡

- Spring Cloud 体系内的客户端负载均衡
- 基于 Ribbon 实现
- 支持轮询、随机、一致性哈希、哈希、响应速度加权、并发量加权、重试等策略

### 3.8. Hystrix（缓存、流控、熔断、降级、统计、监控、告警）

- Spring Cloud 体系内的断路器
- Netflix 团队开源，用于提升整体的可用性和稳定性
- 主要功能：
  - 资源控制（HystrixCommand）（线程池模式和信号量模式，默认使用线程池模式）
  - 缓存（重写 HystrixCommand 的 getCacheKey 方法即可，修改数据时再对应修改缓存）
  - 故障控制
  - 统计/监控/告警
  - 配置热更新

#### 3.8.1. Hystrix 线程机制实现资源控制(Thread)

- 通过线程池的最大线程数、队列长度控制队列长度，同时间请求数超过队列限制或者请求超时，直接走 Fallback 降级
- 缺点：每个 Command 依托线程执行，会增大 CPU 开销

  ```java
  public class GetProductInfoCommand extends HystrixCommand<ProductInfo> {

      private Long productId;

      public GetProductInfoCommand(Long productId) {
          super(HystrixCommandGroupKey.Factory.asKey("GetProductInfoCommandGroup"));
          this.productId = productId;
      }

      @Override
      protected ProductInfo run() {
          String url = "http://localhost:8081/getProductInfo?productId=" + productId;
          // 调用商品服务接口
          String response = HttpClientUtils.sendGetRequest(url);
          return JSONObject.parseObject(response, ProductInfo.class);
      }
  }
  ```

- 调用方式

  ```java
  @RequestMapping("/getProductInfo")
  @ResponseBody
  public String getProductInfo(Long productId) {
      HystrixCommand<ProductInfo> getProductInfoCommand = new GetProductInfoCommand(productId);

      // 通过command执行，获取最新商品数据
      ProductInfo productInfo = getProductInfoCommand.execute();
      System.out.println(productInfo);
      return "success";
  }
  ```

#### 3.8.2. Hystrix 信号量机制实现资源控制(Semaphore)

- 通过信号量控制队列数，同时间请求数超过信号量，或者请求超时，直接走 Fallback 降级
- 缺点： 不能配置 timeout，如果依赖服务延迟严重，会一直处于 block 状态

  ```java
  public class GetCityNameCommand extends HystrixCommand<String> {

      private Long cityId;

      public GetCityNameCommand(Long cityId) {
          // 设置信号量隔离策略
          super(Setter.withGroupKey(HystrixCommandGroupKey.Factory.asKey("GetCityNameGroup"))
                  .andCommandPropertiesDefaults(HystrixCommandProperties.Setter()
                  .withExecutionIsolationStrategy(HystrixCommandProperties.ExecutionIsolationStrategy.SEMAPHORE)));

          this.cityId = cityId;
      }

      @Override
      protected String run() {
          // 需要进行信号量隔离的代码
          return LocationCache.getCityName(cityId);
      }
  }
  ```

- 调用方式：

  ```java
  @RequestMapping("/getProductInfo")
  @ResponseBody
  public String getProductInfo(Long productId) {
      Long cityId = "A1";

      GetCityNameCommand getCityNameCommand = new GetCityNameCommand(cityId);
      // 获取本地内存(cityName)的代码会被信号量进行资源隔离
      String cityName = getCityNameCommand.execute();

      productInfo.setCityName(cityName);

      System.out.println(productInfo);
      return "success";
  }
  ```

#### 3.8.3. Hystrix 细粒度资源控制

- command group：command 组
- command key：每一个 command，都可以设置一个自己的名称 command key，同时可以设置一个自己的组 command group
- command thread pool：ThreadPoolKey 代表了一个 HystrixThreadPool，用来进行统一监控、统计、缓存。默认的 ThreadPoolKey 就是 command group 的名称。每个 command 都会跟它的 ThreadPoolKey 对应的 ThreadPool 绑定在一起

#### 3.8.4. Hystrix 的 fallback（降级）机制

- Hystrix 出现以下三种情况，都会去调用 fallback 降级机制：
  - 断路器处于打开的状态
  - 资源池已满（线程池+队列 / 信号量）
  - 访问外部依赖超时或者出现异常
- 实现方法：
  - 重写 HystrixCommand 的 getFallback 方法
- 常用方案：
  - 读取内存缓存
  - 使用默认值

#### 3.8.5. Hystrix 断路器

- 断路器状态：关闭（Closed）、打开（Open）与半开（Half-Open）
- Closed 断路器关闭：调用下游的请求正常通过
- Open 断路器打开：阻断对下游服务的调用，直接走 Fallback 逻辑
- Half-Open 断路器处于半开状态：一定时间后尝试通过一次请求，如果请求成功，自动恢复 Close 状态
- 断路器触发条件：至少经过多少个请求（可选）、异常比例达到多少（必选）
- 原理：断路器状态由 Close 转换到 Open，在之后 SleepWindowInMilliseconds 时间内，所有经过该断路器的请求会被断路，不调用后端服务，直接走 Fallback 降级机制，默认值 5000ms，之后，断路器会变为 Half-Open 半开闭状态，尝试让一条请求经过断路器，如果请求成功，自动恢复 Close 状态

### 3.9. Task 分布式任务调度

- Spring Cloud 体系内的分布式任务调度器
- 使用关系数据库来存储已执行任务的结果，支持 DB2、H2、MySQL、Oracle、Postgres、SQLServer 等主流关系数据库
- 能与 Spring Batch 集成，将 Spring Batch Job 作为 Task 执行

## 4. <font color=blue>SpringCloud Alibaba</font>

### 4.1. Nacos 服务注册与发现、配置中心、网络远程调用、负载均衡

- Nacos 是阿里巴巴开源的一个动态服务发现、配置管理和服务管理平台
- Nacos 支持几乎所有主流类型的“服务”的发现、配置和管理：
  - Kubernetes Service
  - gRPC & Dubbo RPC Service
  - RESTful Service
- 主要功能：
  - 服务发现和服务健康监测
    - 支持基于 DNS 和基于 RPC 的服务发现
    - 提供对服务的实时的健康检查，阻止向不健康的主机或服务实例发送请求
    - 提供了统一的健康检查仪表盘
  - 动态配置服务
    - 配置中心
  - 动态 DNS 服务
    - 动态路由
    - 负载均衡
    - 流量控制
  - 服务及其元数据管理
    - 管理数据中心的所有服务及元数据，包括管理服务的描述、生命周期、服务的静态依赖分析、服务的健康状态、服务的流量管理、路由及安全策略、服务的 SLA 以及最首要的 metrics 统计数据

### 4.2. Sentinel 限流

- 多样化的流量控制
- 熔断降级
- 系统负载保护
- 实时监控和控制台

### 4.3. Sentinel 和 Hystrix 的区别

- Sentinel 支持注解方式注入规则配置
- Sentinel 可以通过并发线程数模式的流量控制来提供信号量隔离的熔断降级
- Sentinel 支持基于平均响应时间的熔断降级
- Sentinel 支持基于系统负载的熔断降级
- Sentinel 提供了 Metric 指标统计接口
- Sentinel 针对降级还提供了慢启动预热模式（逐渐增加流量到一定阈值）和匀速器模式（严格控制单次请求的时长）
- Sentinel 提供了实时监控和控制面板后台

### 4.4. Seata 分布式事务

### 4.5. SchedulerX 分布式任务调度

### 4.6. RocketMQ 消息总线

- 基于 RocketMQ 实现
