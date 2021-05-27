# <font color=red>JAVA 新技术</font>
<!-- TOC -->

- [<font color=red>JAVA 新技术</font>](#font-colorredjava-%E6%96%B0%E6%8A%80%E6%9C%AFfont)
    - [<font color=blue>响应式编程</font>](#font-colorblue%E5%93%8D%E5%BA%94%E5%BC%8F%E7%BC%96%E7%A8%8Bfont)
        - [简介](#%E7%AE%80%E4%BB%8B)
        - [框架](#%E6%A1%86%E6%9E%B6)
        - [RSocket](#rsocket)
    - [<font color=blue>JAVA 8（LTS 版本（长期支持版本））</font>](#font-colorbluejava-8lts-%E7%89%88%E6%9C%AC%E9%95%BF%E6%9C%9F%E6%94%AF%E6%8C%81%E7%89%88%E6%9C%ACfont)
        - [**函数式接口 FunctionInterface 与 Lambda 表达式**](#%E5%87%BD%E6%95%B0%E5%BC%8F%E6%8E%A5%E5%8F%A3-functioninterface-%E4%B8%8E-lambda-%E8%A1%A8%E8%BE%BE%E5%BC%8F)
        - [**Stream API**](#stream-api)
        - [**接口 default 方法**](#%E6%8E%A5%E5%8F%A3-default-%E6%96%B9%E6%B3%95)
        - [**Date Time API**](#date-time-api)
        - [**反射增强**](#%E5%8F%8D%E5%B0%84%E5%A2%9E%E5%BC%BA)
        - [**Optional 类**](#optional-%E7%B1%BB)
        - [**方法引用**](#%E6%96%B9%E6%B3%95%E5%BC%95%E7%94%A8)
        - [新工具：新的编译工具，如：Nashorn 引擎 jjs、 类依赖分析器 jdeps](#%E6%96%B0%E5%B7%A5%E5%85%B7%E6%96%B0%E7%9A%84%E7%BC%96%E8%AF%91%E5%B7%A5%E5%85%B7%E5%A6%82nashorn-%E5%BC%95%E6%93%8E-jjs-%E7%B1%BB%E4%BE%9D%E8%B5%96%E5%88%86%E6%9E%90%E5%99%A8-jdeps)
        - [Nashorn, JavaScript 引擎](#nashorn-javascript-%E5%BC%95%E6%93%8E)
        - [String.join、Arrays.parallelSort、StampedLock、LongAdder、LongAccumulator 等](#stringjoinarraysparallelsortstampedlocklongadderlongaccumulator-%E7%AD%89)
    - [<font color=blue>JAVA 9</font>（Jigsaw、JShell、Reactive Streams）](#font-colorbluejava-9fontjigsawjshellreactive-streams)
        - [**模块系统：模块是一个包的容器，Java 9 最大的变化之一是引入了模块系统（Jigsaw 项目）**](#%E6%A8%A1%E5%9D%97%E7%B3%BB%E7%BB%9F%E6%A8%A1%E5%9D%97%E6%98%AF%E4%B8%80%E4%B8%AA%E5%8C%85%E7%9A%84%E5%AE%B9%E5%99%A8java-9-%E6%9C%80%E5%A4%A7%E7%9A%84%E5%8F%98%E5%8C%96%E4%B9%8B%E4%B8%80%E6%98%AF%E5%BC%95%E5%85%A5%E4%BA%86%E6%A8%A1%E5%9D%97%E7%B3%BB%E7%BB%9Fjigsaw-%E9%A1%B9%E7%9B%AE)
        - [**REPL JShell：交互式编程环境**](#repl-jshell%E4%BA%A4%E4%BA%92%E5%BC%8F%E7%BC%96%E7%A8%8B%E7%8E%AF%E5%A2%83)
        - [**HTTP 2 客户端**](#http-2-%E5%AE%A2%E6%88%B7%E7%AB%AF)
        - [改进的 Javadoc](#%E6%94%B9%E8%BF%9B%E7%9A%84-javadoc)
        - [多版本兼容 JAR 包](#%E5%A4%9A%E7%89%88%E6%9C%AC%E5%85%BC%E5%AE%B9-jar-%E5%8C%85)
        - [集合工厂方法](#%E9%9B%86%E5%90%88%E5%B7%A5%E5%8E%82%E6%96%B9%E6%B3%95)
        - [私有接口方法](#%E7%A7%81%E6%9C%89%E6%8E%A5%E5%8F%A3%E6%96%B9%E6%B3%95)
        - [进程 API](#%E8%BF%9B%E7%A8%8B-api)
        - [改进的 Stream API](#%E6%94%B9%E8%BF%9B%E7%9A%84-stream-api)
        - [**响应式流（Reactive Streams API**](#%E5%93%8D%E5%BA%94%E5%BC%8F%E6%B5%81reactive-streams-api)
        - [改进 try-with-resources](#%E6%94%B9%E8%BF%9B-try-with-resources)
        - [改进的弃用注解 @Deprecated](#%E6%94%B9%E8%BF%9B%E7%9A%84%E5%BC%83%E7%94%A8%E6%B3%A8%E8%A7%A3-deprecated)
        - [改进钻石操作符Diamond Operator](#%E6%94%B9%E8%BF%9B%E9%92%BB%E7%9F%B3%E6%93%8D%E4%BD%9C%E7%AC%A6diamond-operator)
        - [改进 Optional 类](#%E6%94%B9%E8%BF%9B-optional-%E7%B1%BB)
        - [多分辨率图像 API](#%E5%A4%9A%E5%88%86%E8%BE%A8%E7%8E%87%E5%9B%BE%E5%83%8F-api)
        - [改进的 CompletableFuture API](#%E6%94%B9%E8%BF%9B%E7%9A%84-completablefuture-api)
        - [轻量级的 JSON API](#%E8%BD%BB%E9%87%8F%E7%BA%A7%E7%9A%84-json-api)
    - [<font color=blue>JAVA 10</font>（局部变量类型推断、G1 的并行 Full GC、ThreadLocal 握手机制）](#font-colorbluejava-10font%E5%B1%80%E9%83%A8%E5%8F%98%E9%87%8F%E7%B1%BB%E5%9E%8B%E6%8E%A8%E6%96%ADg1-%E7%9A%84%E5%B9%B6%E8%A1%8C-full-gcthreadlocal-%E6%8F%A1%E6%89%8B%E6%9C%BA%E5%88%B6)
        - [**var 局部变量类型推断**](#var-%E5%B1%80%E9%83%A8%E5%8F%98%E9%87%8F%E7%B1%BB%E5%9E%8B%E6%8E%A8%E6%96%AD)
        - [统一 JDK 仓库](#%E7%BB%9F%E4%B8%80-jdk-%E4%BB%93%E5%BA%93)
        - [**统一垃圾回收接口**](#%E7%BB%9F%E4%B8%80%E5%9E%83%E5%9C%BE%E5%9B%9E%E6%94%B6%E6%8E%A5%E5%8F%A3)
        - [**G1 的并行 Full GC**](#g1-%E7%9A%84%E5%B9%B6%E8%A1%8C-full-gc)
        - [**应用程序类数据 AppCDS 共享**](#%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E7%B1%BB%E6%95%B0%E6%8D%AE-appcds-%E5%85%B1%E4%BA%AB)
        - [**ThreadLocal 握手机制**](#threadlocal-%E6%8F%A1%E6%89%8B%E6%9C%BA%E5%88%B6)
        - [移除 JDK 中附带的 javah 工具。可以使用 javac -h 代替](#%E7%A7%BB%E9%99%A4-jdk-%E4%B8%AD%E9%99%84%E5%B8%A6%E7%9A%84-javah-%E5%B7%A5%E5%85%B7%E5%8F%AF%E4%BB%A5%E4%BD%BF%E7%94%A8-javac--h-%E4%BB%A3%E6%9B%BF)
        - [使用附加的 Unicode 语言标记扩展](#%E4%BD%BF%E7%94%A8%E9%99%84%E5%8A%A0%E7%9A%84-unicode-%E8%AF%AD%E8%A8%80%E6%A0%87%E8%AE%B0%E6%89%A9%E5%B1%95)
        - [能将堆内存占用分配给用户指定的备用内存设备](#%E8%83%BD%E5%B0%86%E5%A0%86%E5%86%85%E5%AD%98%E5%8D%A0%E7%94%A8%E5%88%86%E9%85%8D%E7%BB%99%E7%94%A8%E6%88%B7%E6%8C%87%E5%AE%9A%E7%9A%84%E5%A4%87%E7%94%A8%E5%86%85%E5%AD%98%E8%AE%BE%E5%A4%87)
        - [使用 Graal 基于 Java 的编译器，可以预先把 Java 代码编译成本地代码来提升效能](#%E4%BD%BF%E7%94%A8-graal-%E5%9F%BA%E4%BA%8E-java-%E7%9A%84%E7%BC%96%E8%AF%91%E5%99%A8%E5%8F%AF%E4%BB%A5%E9%A2%84%E5%85%88%E6%8A%8A-java-%E4%BB%A3%E7%A0%81%E7%BC%96%E8%AF%91%E6%88%90%E6%9C%AC%E5%9C%B0%E4%BB%A3%E7%A0%81%E6%9D%A5%E6%8F%90%E5%8D%87%E6%95%88%E8%83%BD)
        - [OpenJDK 中提供一组默认的根证书颁发机构证书](#openjdk-%E4%B8%AD%E6%8F%90%E4%BE%9B%E4%B8%80%E7%BB%84%E9%BB%98%E8%AE%A4%E7%9A%84%E6%A0%B9%E8%AF%81%E4%B9%A6%E9%A2%81%E5%8F%91%E6%9C%BA%E6%9E%84%E8%AF%81%E4%B9%A6)
    - [<font color=blue>JAVA 11（LTS 版本（长期支持版本））</font>（ZGC、Epsilon、增强 var）](#font-colorbluejava-11lts-%E7%89%88%E6%9C%AC%E9%95%BF%E6%9C%9F%E6%94%AF%E6%8C%81%E7%89%88%E6%9C%ACfontzgcepsilon%E5%A2%9E%E5%BC%BA-var)
        - [**用于 Lambda 参数的局部变量语法**](#%E7%94%A8%E4%BA%8E-lambda-%E5%8F%82%E6%95%B0%E7%9A%84%E5%B1%80%E9%83%A8%E5%8F%98%E9%87%8F%E8%AF%AD%E6%B3%95)
        - [**ZGC**](#zgc)
        - [**Epsilon 垃圾回收器**，又被称为"No-Op（无操作）"回收器](#epsilon-%E5%9E%83%E5%9C%BE%E5%9B%9E%E6%94%B6%E5%99%A8%E5%8F%88%E8%A2%AB%E7%A7%B0%E4%B8%BAno-op%E6%97%A0%E6%93%8D%E4%BD%9C%E5%9B%9E%E6%94%B6%E5%99%A8)
        - [低开销的堆分配采样方法](#%E4%BD%8E%E5%BC%80%E9%94%80%E7%9A%84%E5%A0%86%E5%88%86%E9%85%8D%E9%87%87%E6%A0%B7%E6%96%B9%E6%B3%95)
        - [**支持 TLS 1.3**](#%E6%94%AF%E6%8C%81-tls-13)
        - [**标准 HTTP Client 升级**](#%E6%A0%87%E5%87%86-http-client-%E5%8D%87%E7%BA%A7)
        - [基于嵌套的访问控制](#%E5%9F%BA%E4%BA%8E%E5%B5%8C%E5%A5%97%E7%9A%84%E8%AE%BF%E9%97%AE%E6%8E%A7%E5%88%B6)
        - [动态的类文件常量](#%E5%8A%A8%E6%80%81%E7%9A%84%E7%B1%BB%E6%96%87%E4%BB%B6%E5%B8%B8%E9%87%8F)
        - [改进 Aarch64 Intrinsics](#%E6%94%B9%E8%BF%9B-aarch64-intrinsics)
        - [移除 Java EE 和 CORBA 模块，JavaFX 也已被移除](#%E7%A7%BB%E9%99%A4-java-ee-%E5%92%8C-corba-%E6%A8%A1%E5%9D%97javafx-%E4%B9%9F%E5%B7%B2%E8%A2%AB%E7%A7%BB%E9%99%A4)
        - [采用 Curve25519 和 Curve448 算法实现的密钥协议](#%E9%87%87%E7%94%A8-curve25519-%E5%92%8C-curve448-%E7%AE%97%E6%B3%95%E5%AE%9E%E7%8E%B0%E7%9A%84%E5%AF%86%E9%92%A5%E5%8D%8F%E8%AE%AE)
        - [实现 ChaCha20 和 Poly1305 加密算法](#%E5%AE%9E%E7%8E%B0-chacha20-%E5%92%8C-poly1305-%E5%8A%A0%E5%AF%86%E7%AE%97%E6%B3%95)
        - [弃用 Java 8 的 Nashorn JavaScript 引擎](#%E5%BC%83%E7%94%A8-java-8-%E7%9A%84-nashorn-javascript-%E5%BC%95%E6%93%8E)
    - [<font color=blue>JAVA 12</font>（Switch 表达式）](#font-colorbluejava-12fontswitch-%E8%A1%A8%E8%BE%BE%E5%BC%8F)
        - [**Switch 表达式**](#switch-%E8%A1%A8%E8%BE%BE%E5%BC%8F)
        - [Shenandoah GC](#shenandoah-gc)
    - [<font color=blue>JAVA 13</font>（Text Blocks、Dynamic CDS Archives）](#font-colorbluejava-13fonttext-blocksdynamic-cds-archives)
        - [动态应用程序类-数据共享（Dynamic CDS Archives）](#%E5%8A%A8%E6%80%81%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E7%B1%BB-%E6%95%B0%E6%8D%AE%E5%85%B1%E4%BA%ABdynamic-cds-archives)
        - [增强 ZGC 释放未使用内存：Java 13 中对 ZGC 的改进，主要体现在下面几点：](#%E5%A2%9E%E5%BC%BA-zgc-%E9%87%8A%E6%94%BE%E6%9C%AA%E4%BD%BF%E7%94%A8%E5%86%85%E5%AD%98java-13-%E4%B8%AD%E5%AF%B9-zgc-%E7%9A%84%E6%94%B9%E8%BF%9B%E4%B8%BB%E8%A6%81%E4%BD%93%E7%8E%B0%E5%9C%A8%E4%B8%8B%E9%9D%A2%E5%87%A0%E7%82%B9)
        - [Socket API 重构](#socket-api-%E9%87%8D%E6%9E%84)
        - [Switch 表达式扩展（预览功能）](#switch-%E8%A1%A8%E8%BE%BE%E5%BC%8F%E6%89%A9%E5%B1%95%E9%A2%84%E8%A7%88%E5%8A%9F%E8%83%BD)
        - [文本块（Text Blocks，预览功能）](#%E6%96%87%E6%9C%AC%E5%9D%97text-blocks%E9%A2%84%E8%A7%88%E5%8A%9F%E8%83%BD)
    - [<font color=blue>JAVA 14</font>（Java 打包工具、NullPointerException、record 类型）](#font-colorbluejava-14fontjava-%E6%89%93%E5%8C%85%E5%B7%A5%E5%85%B7nullpointerexceptionrecord-%E7%B1%BB%E5%9E%8B)
        - [**优化 instanceof 的模式匹配**](#%E4%BC%98%E5%8C%96-instanceof-%E7%9A%84%E6%A8%A1%E5%BC%8F%E5%8C%B9%E9%85%8D)
        - [**Java 打包工具（孵化项目）**](#java-%E6%89%93%E5%8C%85%E5%B7%A5%E5%85%B7%E5%AD%B5%E5%8C%96%E9%A1%B9%E7%9B%AE)
        - [**G1 GC 支持 NUMA**](#g1-gc-%E6%94%AF%E6%8C%81-numa)
        - [**更有价值的 NullPointerException**](#%E6%9B%B4%E6%9C%89%E4%BB%B7%E5%80%BC%E7%9A%84-nullpointerexception)
        - [**记录类型（Record Type，预览功能）**](#%E8%AE%B0%E5%BD%95%E7%B1%BB%E5%9E%8Brecord-type%E9%A2%84%E8%A7%88%E5%8A%9F%E8%83%BD)
        - [**正式引入 JDK 12 的 Switch 表达式**](#%E6%AD%A3%E5%BC%8F%E5%BC%95%E5%85%A5-jdk-12-%E7%9A%84-switch-%E8%A1%A8%E8%BE%BE%E5%BC%8F)
        - [**正式引入 JDK 13 的 Text Blocks（文本框）功能**](#%E6%AD%A3%E5%BC%8F%E5%BC%95%E5%85%A5-jdk-13-%E7%9A%84-text-blocks%E6%96%87%E6%9C%AC%E6%A1%86%E5%8A%9F%E8%83%BD)
        - [**ZGC 的 macOS 支持和 Windows 支持**](#zgc-%E7%9A%84-macos-%E6%94%AF%E6%8C%81%E5%92%8C-windows-%E6%94%AF%E6%8C%81)
        - [新增外部内存地址访 API（MemorySegment、MemoryAddress 和 MemoryLayout）](#%E6%96%B0%E5%A2%9E%E5%A4%96%E9%83%A8%E5%86%85%E5%AD%98%E5%9C%B0%E5%9D%80%E8%AE%BF-apimemorysegmentmemoryaddress-%E5%92%8C-memorylayout)
        - [新增指向 NVM（non-volatile memory，非易失性内存）的 MappedByteBuffer](#%E6%96%B0%E5%A2%9E%E6%8C%87%E5%90%91-nvmnon-volatile-memory%E9%9D%9E%E6%98%93%E5%A4%B1%E6%80%A7%E5%86%85%E5%AD%98%E7%9A%84-mappedbytebuffer)
        - [新增 JRF（Java Flight Recorder）事件流](#%E6%96%B0%E5%A2%9E-jrfjava-flight-recorder%E4%BA%8B%E4%BB%B6%E6%B5%81)
        - [**删除 CMS 垃圾回收器**](#%E5%88%A0%E9%99%A4-cms-%E5%9E%83%E5%9C%BE%E5%9B%9E%E6%94%B6%E5%99%A8)
        - [废弃 ParallelScavenge + SerialOld 的 GC 组合](#%E5%BA%9F%E5%BC%83-parallelscavenge--serialold-%E7%9A%84-gc-%E7%BB%84%E5%90%88)

<!-- /TOC -->
## 1. <font color=blue>响应式编程</font>

### 1.1. 简介

- 响应式编程为 Java 的企业版应用提供了更高的性能，并降低了内存消耗
- 主要是通过减少进程的上下文切换（将耗时的 IO 操作变成异步）来实现的。因为类似的上下文切换对 CPU 和内存的消耗是极大，所以要尽可能的减少这样的切换操作
- 不过，响应式编程带来的这种性能上的提高，代价是降低了软件的维护性

### 1.2. 框架

- Java 8 的 Stream 流，Observable 和 Observer 模式
- RxJava：移动端用的较多的框架，基于观察者模式
- WebFlux：Flux 和 Mono，Flux 主要是针对 0-N 的元素，Mono 主要是针对 0-1 个元素
- Reactor：类似 WebFlux

### 1.3. RSocket

- 一种二进制的点对点通信协议，是一种新的网络通信第七层（应用层）协议
- 旨在用于分布式应用程序中，是 HTTP 等其他协议的替代方案
- 基于 Reactive Streams 规范具有异步，多路复用，断线重连，基于消息等特性
- 它由 Facebook，Netifi 和 Pivotal 等工程师开发，提供 Java，JavaScript，C ++和 Kotlin 等实现，Spring framework 最近的几次更新都特别对其进行了支持。知名 rpc 框架 Dubbo 从 3 开始也针对 RSocket 进行了适配
- RSocket 定义了四种交互模型来弥补 Http 协议的不足之处：
  - Fire-and-Forget：优化请求/响应，在不需要响应时非常有用，例如非关键事件日志记录
  - Request/Response：类似 Http 的请求/响应模型 但是具有 Http 没有的优点，它是异步和多路复用的
  - Request/Stream：单个请求可以接收多个响应。例如获取视频列表、获取目录中的产品
  - Channel: 该模型模型提供双向通信。在此模型中，消息流在两个方向上异步流动。例如发生更改时，从服务器向客户端发出增量/差异

## 2. <font color=blue>JAVA 8（LTS 版本（长期支持版本））</font>

### 2.1. **函数式接口 FunctionInterface 与 Lambda 表达式**

函数式编程，允许把函数作为一个方法的参数（例：(parameters) -> expression）

### 2.2. **Stream API**

新添加的 Stream API（java.util.stream） 把真正的函数式编程风格引入到 Java 中

### 2.3. **接口 default 方法**

接口里面可以直接实现方法

### 2.4. **Date Time API**

加强对日期与时间的处理

### 2.5. **反射增强**

可以通过反射来获取方法的参数名

### 2.6. **Optional 类**

Optional 类已经成为 Java 8 类库的一部分，用来解决空指针异常

### 2.7. **方法引用**

方法引用提供了非常有用的语法，可以直接引用已有 Java 类或对象（实例）的方法或构造器。与 lambda 联合使用，方法引用可以使语言的构造更紧凑简洁，减少冗余代码（例：System.out::print）

### 2.8. 新工具：新的编译工具，如：Nashorn 引擎 jjs、 类依赖分析器 jdeps

### 2.9. Nashorn, JavaScript 引擎

Java 8 提供了一个新的 Nashorn javascript 引擎，它允许我们在 JVM 上运行特定的 javascript 应用

### 2.10. String.join、Arrays.parallelSort、StampedLock、LongAdder、LongAccumulator 等

## 3. <font color=blue>JAVA 9</font>（Jigsaw、JShell、Reactive Streams）

### 3.1. **模块系统：模块是一个包的容器，Java 9 最大的变化之一是引入了模块系统（Jigsaw 项目）**
### 3.2. **REPL (JShell)：交互式编程环境**

- JShell 是 Java 9 新增的一个交互式的编程环境工具
- 它允许你无需使用类或者方法包装来执行 Java 语句
- 它与 Python 的解释器类似，可以直接 输入表达式并查看其执行结果

### 3.3. **HTTP 2 客户端**

HTTP/2 标准是 HTTP 协议的最新版本，新的 HTTPClient API 支持 WebSocket 和 HTTP2 流以及服务器推送特性

### 3.4. 改进的 Javadoc

Javadoc 现在支持在 API 文档中的进行搜索。另外，Javadoc 的输出现在符合兼容 HTML5 标准

### 3.5. 多版本兼容 JAR 包

多版本兼容 JAR 功能能让你创建仅在特定版本的 Java 环境中运行库程序时选择使用的 class 版本

### 3.6. 集合工厂方法

List，Set 和 Map 接口中，新的静态工厂方法可以创建这些集合的不可变实例

### 3.7. 私有接口方法

在接口中使用 private 私有方法。我们可以使用 private 访问修饰符在接口中编写私有方法

### 3.8. 进程 API

改进的 API 来控制和管理操作系统进程。引进 java.lang.ProcessHandle 及其嵌套接口 Info 来让开发者逃离时常因为要获取一个本地进程的 PID 而不得不使用本地代码的窘境

### 3.9. 改进的 Stream API

改进的 Stream API 添加了一些便利的方法，使流处理更容易，并使用收集器编写复杂的查询

### 3.10. **响应式流（Reactive Streams) API**

Java 9 中引入了新的响应式流 API 来支持 Java 9 中的响应式编程

### 3.11. 改进 try-with-resources

如果你已经有一个资源是 final 或等效于 final 变量,您可以在 try-with-resources 语句中使用该变量，而无需在 try-with-resources 语句中声明一个新变量

### 3.12. 改进的弃用注解 @Deprecated

注解 @Deprecated 可以标记 Java API 状态，可以表示被标记的 API 将会被移除，或者已经破坏

### 3.13. 改进钻石操作符(Diamond Operator) 

匿名类可以使用钻石操作符(Diamond Operator)

### 3.14. 改进 Optional 类

java.util.Optional 添加了很多新的有用方法，Optional 可以直接转为 stream

### 3.15. 多分辨率图像 API

定义多分辨率图像 API，开发者可以很容易的操作和展示不同分辨率的图像了

### 3.16. 改进的 CompletableFuture API

CompletableFuture 类的异步机制可以在 ProcessHandle.onExit 方法退出时执行操作

### 3.17. 轻量级的 JSON API

内置了一个轻量级的 JSON API

## 4. <font color=blue>JAVA 10</font>（局部变量类型推断、G1 的并行 Full GC、ThreadLocal 握手机制）

### 4.1. **var 局部变量类型推断**

引入"var"关键字，可以随意定义变量而不必指定变量的类型

### 4.2. 统一 JDK 仓库

将原来用 Mercurial 管理的众多 JDK 仓库代码，合并到一个仓库中，简化开发和管理过程

### 4.3. **统一垃圾回收接口**

引入一个纯净的垃圾收集器接口，以帮助改进不同垃圾收集器的源代码隔离

### 4.4. **G1 的并行 Full GC**

截止到 Java 9，G1 的 Full GC 采用的是单线程算法，Java10 开始，在发生 Full GC 时可以使用多个线程进行并行回收

### 4.5. **应用程序类数据 (AppCDS) 共享**

通过跨进程共享通用类元数据来减少内存占用空间，和减少启动时间

### 4.6. **ThreadLocal 握手机制**

在不进入到全局 JVM 安全点 (Safepoint) 的情况下，对线程执行回调。优化可以只停止单个线程，而不是停全部线程或一个都不停

### 4.7. 移除 JDK 中附带的 javah 工具。可以使用 javac -h 代替

### 4.8. 使用附加的 Unicode 语言标记扩展

### 4.9. 能将堆内存占用分配给用户指定的备用内存设备

### 4.10. 使用 Graal 基于 Java 的编译器，可以预先把 Java 代码编译成本地代码来提升效能

### 4.11. OpenJDK 中提供一组默认的根证书颁发机构证书

开源目前 Oracle 提供的的 Java SE 的根证书，这样 OpenJDK 对开发人员使用起来更方便

## 5. <font color=blue>JAVA 11（LTS 版本（长期支持版本））</font>（ZGC、Epsilon、增强 var）

### 5.1. **用于 Lambda 参数的局部变量语法**

可以在 Lambda 表达式中使用 var，提高代码可读性（例如：(var x, var y) -> x.process(y)）

### 5.2. **ZGC**

- ZGC 即 Z Garbage Collector，处于实验性阶段，只在 Linux/x64 上可用
- ZGC 是一个可伸缩的、低延迟的垃圾收集器
- 主要为了满足如下目标进行设计：
  - GC 停顿时间不超过 10ms
  - 即能处理几百 MB 的小堆，也能处理几个 TB 的大堆
  - 应用吞吐能力不会下降超过 15%（与 G1 回收算法相比）

### 5.3. **Epsilon 垃圾回收器**，又被称为"No-Op（无操作）"回收器

- Epsilon 垃圾回收器的目标是开发一个控制内存分配，但是不执行任何实际的垃圾回收工作
- 它提供一个完全消极的 GC 实现，分配有限的内存资源，最大限度的降低内存占用和内存吞吐延迟时间
- 主要使用场景；
  - 性能测试
  - 内存压力测试
  - VM 接口测试
  - 延迟和吞吐量改进

### 5.4. 低开销的堆分配采样方法

Java 11 中提供一种低开销的 Java 堆分配采样方法，能够得到堆分配的 Java 对象信息，并且能够通过 JVMTI 访问堆信息

### 5.5. **支持 TLS 1.3**

### 5.6. **标准 HTTP Client 升级**

- 提供了对 HTTP/2 等业界前沿标准的支持，同时也向下兼容 HTTP/1.1
- 精简而又友好的 API 接口，与主流开源 API（如：Apache HttpClient、Jetty、OkHttp 等）类似甚至拥有更高的性能
- 它是 Java 在 Reactive-Stream 方面的第一个生产实践

### 5.7. 基于嵌套的访问控制

### 5.8. 动态的类文件常量

### 5.9. 改进 Aarch64 Intrinsics

### 5.10. 移除 Java EE 和 CORBA 模块，JavaFX 也已被移除

### 5.11. 采用 Curve25519 和 Curve448 算法实现的密钥协议

### 5.12. 实现 ChaCha20 和 Poly1305 加密算法

### 5.13. 弃用 Java 8 的 Nashorn JavaScript 引擎

## 6. <font color=blue>JAVA 12</font>（Switch 表达式）

### 6.1. **Switch 表达式**
  
  ```java
  switch (day) {
      case MONDAY, FRIDAY, SUNDAY -> System.out.println(6);
      case TUESDAY                -> System.out.println(7);
      case THURSDAY, SATURDAY     -> System.out.println(8);
      case WEDNESDAY              -> System.out.println(9);
  }
  ```

### 6.2. Shenandoah GC

- 是 Redhat 主导开发的 Pauseless GC 实现
- 主要目标是 99.9% 的暂停小于 10ms，以及可以处理大堆和小堆
- 是一个实验性功能，不包含在默认（Oracle）的 OpenJDK 版本中

## 7. <font color=blue>JAVA 13</font>（Text Blocks、Dynamic CDS Archives）

### 7.1. 动态应用程序类-数据共享（Dynamic CDS Archives）

- Java 13 中对 Java 10 中引入的 应用程序类数据共享进行了进一步的简化、改进和扩展
- 允许在 Java 应用程序执行结束时动态进行类归档
- 具体能够被归档的类包括：所有已被加载，但不属于默认基层 CDS 的应用程序类和引用类库中的类
- 通过这种改进，可以提高应用程序类-数据使用上的简易性，减少在使用类-数据存档中需要为应用程序创建类加载列表的必要，简化使用类-数据共享的步骤，以便更简单、便捷地使用 CDS 存档

### 7.2. 增强 ZGC 释放未使用内存：Java 13 中对 ZGC 的改进，主要体现在下面几点：

- 释放未使用内存给操作系统
- 释放未使用内存给操作系统
- 添加参数：-XX:SoftMaxHeapSize 来软限制堆大小

### 7.3. Socket API 重构

- Java 13 为 Socket API 带来了新的底层实现方法，并且在 Java 13 中是默认使用新的 Socket 实现，使其易于发现并在排除问题同时增加可维护性

### 7.4. Switch 表达式扩展（预览功能）

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

### 7.5. 文本块（Text Blocks，预览功能）

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

## 8. <font color=blue>JAVA 14</font>（Java 打包工具、NullPointerException、record 类型）

### 8.1. **优化 instanceof 的模式匹配**

  ```java
  void patternMatching(Object obj) {
    if (obj instanceof String str) {
      System.out.println(str.length());
    }
  }
  ```

### 8.2. **Java 打包工具（孵化项目）**

- 使用 jpackage 命令打包，可以将 jar 文件打包成 exe、rpm、dmg 格式的可执行文件

### 8.3. **G1 GC 支持 NUMA**

- 优化了 G1 在使用 NUMA（non-uniform memory access）时的内存分配

### 8.4. **更有价值的 NullPointerException**

- JAVA 14 增强了对 NullPointerException 异常的处理，可以显示详细的信息，错误消息可以明确的指出为空的对象
- 这个功能需要通过选项-XX:+ShowCodeDetailsInExceptionMessages 启用

### 8.5. **记录类型（Record Type，预览功能）**

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

### 8.6. **正式引入 JDK 12 的 Switch 表达式**

### 8.7. **正式引入 JDK 13 的 Text Blocks（文本框）功能**

### 8.8. **ZGC 的 macOS 支持和 Windows 支持**

### 8.9. 新增外部内存地址访 API（MemorySegment、MemoryAddress 和 MemoryLayout）

### 8.10. 新增指向 NVM（non-volatile memory，非易失性内存）的 MappedByteBuffer

### 8.11. 新增 JRF（Java Flight Recorder）事件流

### 8.12. **删除 CMS 垃圾回收器**

- Concurrent Mark Sweep（CMS）垃圾回收器在 JDK 9 中被声明为废弃的。在 JDK 14 中，CMS 被移除

### 8.13. 废弃 ParallelScavenge + SerialOld 的 GC 组合
