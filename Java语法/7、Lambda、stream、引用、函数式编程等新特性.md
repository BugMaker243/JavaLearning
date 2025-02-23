# JDK8-17新特性

> Lambda、stream、引用、函数式编程等新特性

## 1. Java版本介绍与认识

### 1.1 名词解释

#### 1.1.1 名词解释：Oracle JDK和Open JDK

这两个JDK最大不同就是许可证不一样。**但是对于个人用户来讲，没区别。**

|              | Oracle JDK                                                   | Open JDK                  |
| ------------ | ------------------------------------------------------------ | ------------------------- |
| 来源         | Oracle团队维护                                               | Oracle和Open Java社区     |
| 授权协议     | Java 17及更高版本 Oracle Java SE 许可证<br>Java16及更低版本甲骨文免费条款和条件 （NFTC） 许可协议 | GPL v2许可证              |
| 关系         | 由Open JDK构建，增加了少许内容                               |                           |
| 是否收费     | 2021年9月起Java17及更高版本所有用户免费。 16及更低版本，个人用户、开发用户免费。 | 2017年9月起，所有版本免费 |
| 对语法的支持 | 一致                                                         | 一致                      |

#### 1.1.2 名词解释：JEP

JEP(JDK Enhancement Proposals)：jdk 改进提案，每当需要有新的设想时候，JEP可以提出非正式的规范(specification)，被正式认可的JEP正式写进JDK的发展路线图并分配版本号。

#### 1.1.3 名词解释：LTS

LTS（Long-term Support）即长期支持。Oracle官网提供了对Oracle JDK个别版本的长期支持，即使发发行了新版本，比如目前最新的JDK19，在结束日期前，LTS版本都会被长期支持。（出了bug，会被修复，非LTS则不会再有补丁发布）所以，一定要选一个LTS版本，不然出了漏洞没人修复了。

| 版本      | 开始日期  | 结束日期  | 延期结束日期 |
| --------- | --------- | --------- | ------------ |
| 7（LTS）  | 2011年7月 | 2019年7月 | 2022年7月    |
| 8（LTS）  | 2014年3月 | 2022年3月 | 2030年12月   |
| 11（LTS） | 2018年9月 | 2023年9月 | 2026年9月    |
| 17（LTS） | 2021年9月 | 2026年9月 | 2029年9月    |
| 21（LTS） | 2023年9月 | 2028年9月 | 2031年9月    |

如果要选择Oracle JDK，目前可选的LTS版本为8、11、17三个。

### 1.2 各版本新增特性简述

#### jdk 9

Java 9 提供了`超过150项`新功能特性，包括备受期待的模块化系统、可交互的 REPL 工具：jshell，JDK 编译工具，Java 公共 API 和私有代码，以及安全增强、扩展提升、性能管理改善等。

特性太多，查看链接：

https://openjdk.java.net/projects/jdk9/

#### jdk 10

https://openjdk.java.net/projects/jdk/10/

> 286: [Local-Variable Type Inference](http://openjdk.java.net/jeps/286) 局部变量类型推断
> 296: [Consolidate the JDK Forest into a Single Repository](http://openjdk.java.net/jeps/296) JDK库的合并
> 304: [Garbage-Collector Interface](http://openjdk.java.net/jeps/304) 统一的垃圾回收接口
> 307: [Parallel Full GC for G1](http://openjdk.java.net/jeps/307) 为G1提供并行的Full GC
> 310: [Application Class-Data Sharing](http://openjdk.java.net/jeps/310) 应用程序类数据（AppCDS）共享
> 312: [Thread-Local Handshakes](http://openjdk.java.net/jeps/312) ThreadLocal握手交互
> 313: [Remove the Native-Header Generation Tool (javah)](http://openjdk.java.net/jeps/313) 移除JDK中附带的javah工具
> 314: [Additional Unicode Language-Tag Extensions](http://openjdk.java.net/jeps/314) 使用附加的Unicode语言标记扩展
> 316: [Heap Allocation on Alternative Memory Devices](http://openjdk.java.net/jeps/316) 能将堆内存占用分配给用户指定的备用内存设备
> 317: [Experimental Java-Based JIT Compiler](http://openjdk.java.net/jeps/317) 使用Graal基于Java的编译器
>
> 319: [Root Certificates](http://openjdk.java.net/jeps/319) 根证书
> 322: [Time-Based Release Versioning](http://openjdk.java.net/jeps/322) 基于时间定于的发布版本

#### jdk 11

https://openjdk.java.net/projects/jdk/11/

> 181: [Nest-Based Access Control](https://openjdk.java.net/jeps/181)  基于嵌套的访问控制
> 309: [Dynamic Class-File Constants](https://openjdk.java.net/jeps/309) 动态类文件常量
> 315: [Improve Aarch64 Intrinsics](https://openjdk.java.net/jeps/315) 改进 Aarch64 Intrinsics
> 318: [Epsilon: A No-Op Garbage Collector](https://openjdk.java.net/jeps/318) Epsilon — 一个No-Op（无操作）的垃圾收集器
> 320: [Remove the Java EE and CORBA Modules](https://openjdk.java.net/jeps/320) 删除 Java EE 和 CORBA 模块
> 321: [HTTP Client (Standard)](https://openjdk.java.net/jeps/321)  HTTPClient API
> 323: [Local-Variable Syntax for Lambda Parameters](https://openjdk.java.net/jeps/323)  用于 Lambda 参数的局部变量语法
> 324: [Key Agreement with Curve25519 and Curve448](https://openjdk.java.net/jeps/324) Curve25519 和 Curve448 算法的密钥协议
> 327: [Unicode 10](https://openjdk.java.net/jeps/327)
> 328: [Flight Recorder](https://openjdk.java.net/jeps/328) 飞行记录仪
> 329: [ChaCha20 and Poly1305 Cryptographic Algorithms](https://openjdk.java.net/jeps/329) ChaCha20 和 Poly1305 加密算法
> 330: [Launch Single-File Source-Code Programs](https://openjdk.java.net/jeps/330) 启动单一文件的源代码程序
> 331: [Low-Overhead Heap Profiling](https://openjdk.java.net/jeps/331) 低开销的 Heap Profiling
> 332: [Transport Layer Security (TLS) 1.3](https://openjdk.java.net/jeps/332) 支持 TLS 1.3
> 333: [ZGC: A Scalable Low-Latency Garbage Collector
>    (Experimental)](https://openjdk.java.net/jeps/333) 可伸缩低延迟垃圾收集器
> 335: [Deprecate the Nashorn JavaScript Engine](https://openjdk.java.net/jeps/335) 弃用 Nashorn JavaScript 引擎
> 336: [Deprecate the Pack200 Tools and API](https://openjdk.java.net/jeps/336)  弃用 Pack200 工具和 API

#### jdk 12

https://openjdk.java.net/projects/jdk/12/

> 189：[Shenandoah: A Low-Pause-Time Garbage Collector (Experimental)](https://openjdk.java.net/jeps/189) 低暂停时间的GC
> 230: [Microbenchmark Suite](https://openjdk.java.net/jeps/230) 微基准测试套件
> 325: [Switch Expressions (Preview)](https://openjdk.java.net/jeps/325) switch表达式
> 334: [JVM Constants API ](https://openjdk.java.net/jeps/334) JVM常量API
> 340: [One AArch64 Port, Not Two](https://openjdk.java.net/jeps/340) 只保留一个AArch64实现
> 341: [Default CDS Archives](https://openjdk.java.net/jeps/341) 默认类数据共享归档文件
> 344: [Abortable Mixed Collections for G1](https://openjdk.java.net/jeps/344) 可中止的G1 Mixed GC
> 346: [Promptly Return Unused Committed Memory from G1](https://openjdk.java.net/jeps/346) G1及时返回未使用的已分配内存

#### jdk 13

https://openjdk.java.net/projects/jdk/13/

> 350: [Dynamic CDS Archives](https://openjdk.java.net/jeps/350) 动态CDS档案
> 351: [ZGC: Uncommit Unused Memory](https://openjdk.java.net/jeps/351) ZGC:取消使用未使用的内存
> 353: [Reimplement the Legacy Socket API](https://openjdk.java.net/jeps/353) 重新实现旧版套接字API
> 354: [Switch Expressions (Preview)](https://openjdk.java.net/jeps/354) switch表达式（预览）
> 355: [Text Blocks (Preview)](https://openjdk.java.net/jeps/355) 文本块（预览）

#### jdk 14

https://openjdk.java.net/projects/jdk/14/

> 305: [Pattern Matching for instanceof (Preview)](https://openjdk.java.net/jeps/305) instanceof的模式匹配
> 343: [Packaging Tool (Incubator)](https://openjdk.java.net/jeps/343) 打包工具
> 345: [NUMA-Aware Memory Allocation for G1](https://openjdk.java.net/jeps/345) G1的NUMA-Aware内存分配
> 349: [JFR Event Streaming](https://openjdk.java.net/jeps/349) JFR事件流
> 352: [Non-Volatile Mapped Byte Buffers](https://openjdk.java.net/jeps/352) 非易失性映射字节缓冲区
> 358: [Helpful NullPointerExceptions](https://openjdk.java.net/jeps/358) 实用的NullPointerExceptions
> 359: [Records (Preview)](https://openjdk.java.net/jeps/359) 
> 361: [Switch Expressions (Standard)](https://openjdk.java.net/jeps/361) Switch表达式
> 362: [Deprecate the Solaris and SPARC Ports](https://openjdk.java.net/jeps/362) 弃用Solaris和SPARC端口
> 363: [Remove the Concurrent Mark Sweep (CMS) Garbage Collector](https://openjdk.java.net/jeps/363) 删除并发标记扫描（CMS）垃圾回收器
> 364: [ZGC on macOS](https://openjdk.java.net/jeps/364) 
> 365: [ZGC on Windows](https://openjdk.java.net/jeps/365) 
> 366: [Deprecate the ParallelScavenge + SerialOld GC Combination](https://openjdk.java.net/jeps/366) 弃用ParallelScavenge + SerialOld GC组合
> 367: [Remove the Pack200 Tools and API](https://openjdk.java.net/jeps/367) 删除Pack200工具和API
> 368: [Text Blocks (Second Preview)](https://openjdk.java.net/jeps/368) 文本块
> 370: [Foreign-Memory Access API (Incubator)](https://openjdk.java.net/jeps/370) 外部存储器访问API

#### jdk 15

https://openjdk.java.net/projects/jdk/15/

> 339: [Edwards-Curve Digital Signature Algorithm (EdDSA)](https://openjdk.java.net/jeps/339) EdDSA 数字签名算法
> 360: [Sealed Classes (Preview)](https://openjdk.java.net/jeps/360) 密封类（预览）
> 371: [Hidden Classes](https://openjdk.java.net/jeps/371) 隐藏类
> 372: [Remove the Nashorn JavaScript Engine](https://openjdk.java.net/jeps/372) 移除 Nashorn JavaScript 引擎
> 373: [Reimplement the Legacy DatagramSocket API](https://openjdk.java.net/jeps/373) 重新实现 Legacy DatagramSocket API
> 374: [Disable and Deprecate Biased Locking](https://openjdk.java.net/jeps/374) 禁用偏向锁定
> 375: [Pattern Matching for instanceof (Second Preview)](https://openjdk.java.net/jeps/375) instanceof 模式匹配（第二次预览）
> 377: [ZGC: A Scalable Low-Latency Garbage Collector](https://openjdk.java.net/jeps/377) ZGC：一个可扩展的低延迟垃圾收集器
> 378: [Text Blocks](https://openjdk.java.net/jeps/378) 文本块
> 379: [Shenandoah: A Low-Pause-Time Garbage Collector](https://openjdk.java.net/jeps/379) Shenandoah:低暂停时间垃圾收集器
> 381: [Remove the Solaris and SPARC Ports](https://openjdk.java.net/jeps/381) 移除 Solaris 和 SPARC 端口
> 383: [Foreign-Memory Access API (Second Incubator)](https://openjdk.java.net/jeps/383) 外部存储器访问 API（第二次孵化版）
> 384: [Records (Second Preview)](https://openjdk.java.net/jeps/384) Records（第二次预览）
> 385: [Deprecate RMI Activation for Removal](https://openjdk.java.net/jeps/385) 废弃 RMI 激活机制

#### jdk 16

https://openjdk.java.net/projects/jdk/16/

> 338: [Vector API (Incubator)](https://openjdk.java.net/jeps/338) Vector API（孵化器）
> 347: [Enable C++14 Language Features](https://openjdk.java.net/jeps/347) JDK C++的源码中允许使用C++14的语言特性
> 357: [Migrate from Mercurial to Git](https://openjdk.java.net/jeps/357) OpenJDK源码的版本控制从Mercurial (hg) 迁移到git
> 369: [Migrate to GitHub](https://openjdk.java.net/jeps/369) OpenJDK源码的版本控制迁移到github上
> 376: [ZGC: Concurrent Thread-Stack Processing](https://openjdk.java.net/jeps/376) ZGC：并发线程处理
> 380: [Unix-Domain Socket Channels](https://openjdk.java.net/jeps/380) Unix域套接字通道
> 386: [Alpine Linux Port](https://openjdk.java.net/jeps/386) 将glibc的jdk移植到使用musl的alpine linux上
> 387: [Elastic Metaspace](https://openjdk.java.net/jeps/387) 弹性元空间
> 388: [Windows/AArch64 Port](https://openjdk.java.net/jeps/388) 移植JDK到Windows/AArch64
> 389: [Foreign Linker API (Incubator)](https://openjdk.java.net/jeps/389) 提供jdk.incubator.foreign来简化native code的调用
> 390: [Warnings for Value-Based Classes](https://openjdk.java.net/jeps/390) 提供基于值的类的警告
> 392: [Packaging Tool](https://openjdk.java.net/jeps/392) jpackage打包工具转正
> 393: [Foreign-Memory Access API (Third Incubator)](https://openjdk.java.net/jeps/393) 
> 394: [Pattern Matching for instanceof](https://openjdk.java.net/jeps/394) Instanceof的模式匹配转正
> 395: [Records](https://openjdk.java.net/jeps/395) Records转正
> 396: [Strongly Encapsulate JDK Internals by Default](https://openjdk.java.net/jeps/396) 默认情况下，封装了JDK内部构件
> 397: [Sealed Classes (Second Preview)](https://openjdk.java.net/jeps/397) 密封类

#### jdk 17

https://openjdk.java.net/projects/jdk/17/

> 306: [Restore Always-Strict Floating-Point Semantics](https://openjdk.java.net/jeps/306) 恢复始终严格的浮点语义
>
> 356: [Enhanced Pseudo-Random Number Generators](https://openjdk.java.net/jeps/356) 增强型伪随机数生成器
>
> 382: [New macOS Rendering Pipeline](https://openjdk.java.net/jeps/382) 新的macOS渲染管道
>
> 391: [macOS/AArch64 Port](https://openjdk.java.net/jeps/391) macOS/AArch64端口
>
> 398: [Deprecate the Applet API for Removal](https://openjdk.java.net/jeps/398) 弃用Applet API后续将进行删除
>
> 403: [Strongly Encapsulate JDK Internals](https://openjdk.java.net/jeps/403) 强封装JDK的内部API
>
> 406: [Pattern Matching for switch (Preview)](https://openjdk.java.net/jeps/406) switch模式匹配（预览）
>
> 407: [Remove RMI Activation](https://openjdk.java.net/jeps/407) 删除RMI激活机制
>
> 409: [Sealed Classes](https://openjdk.java.net/jeps/409) 密封类转正
>
> 410: [Remove the Experimental AOT and JIT Compiler](https://openjdk.java.net/jeps/410) 删除实验性的AOT和JIT编译器
>
> 411: [Deprecate the Security Manager for Removal](https://openjdk.java.net/jeps/411) 弃用即将删除的安全管理器
>
> 412: [Foreign Function & Memory API (Incubator)](https://openjdk.java.net/jeps/412) 外部函数和内存API（孵化特性）
>
> 414: [Vector API (Second Incubator)](https://openjdk.java.net/jeps/414) Vector API（第二次孵化特性）
>
> 415: [Context-Specific Deserialization Filters](https://openjdk.java.net/jeps/415) 上下文特定的反序列化过滤器

### 1.3 如何学习新特性

对于新特性，我们应该从哪几个角度学习新特性呢？

- 语法层面：
  - 比如JDK5中的自动拆箱、自动装箱、enum、泛型
  - 比如JDK8中的lambda表达式、接口中的默认方法、静态方法
  - 比如JDK10中局部变量的类型推断
  - 比如JDK12中的switch
  - 比如JDK13中的文本块
- API层面：
  - 比如JDK8中的Stream、Optional、新的日期时间、HashMap的底层结构
  - 比如JDK9中String的底层结构
  - 新的 / 过时的 API
- 底层优化
  - 比如JDK8中永久代被元空间替代、新的JS执行引擎
  - 比如新的垃圾回收器、GC参数、JVM的优化

## 2. Java8新特性：Lambda表达式

### 2.1 关于Java8新特性简介

Java 8 (又称为 JDK 8或JDK1.8) 是 Java 语言开发的一个主要版本。 Java 8 是oracle公司于2014年3月发布，可以看成是自Java 5 以来最具革命性的版本。Java 8为Java语言、编译器、类库、开发工具与JVM带来了大量新特性。

<img src="http://jason243.online/javase_songhongkang/images/image-20220525201653599.png" alt="image-20220525201653599" style="zoom:80%;" />

- 速度更快
- 代码更少(增加了新的语法：**Lambda** **表达式**)
- 强大的 **Stream API**
- 便于并行
  - **并行流**就是把一个内容分成多个数据块，并用不同的线程分别处理每个数据块的流。相比较串行的流，并行的流可以很大程度上提高程序的执行效率。
  - Java 8 中将并行进行了优化，我们可以很容易的对数据进行并行操作。Stream API 可以声明性地通过 parallel() 与 sequential() 在并行流与顺序流之间进行切换。
- 最大化减少空指针异常：Optional

### 2.2 使用Lambda表达式的原因：消除冗余的匿名内部类

当需要启动一个线程去完成任务时，通常会通过`java.lang.Runnable`接口来定义任务内容，并使用`java.lang.Thread`类来启动该线程。代码如下：

```java
package com.atguigu.fp;

public class UseFunctionalProgramming {
    public static void main(String[] args) {
        new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("多线程任务执行！");
            }
        }).start(); // 启动线程
    }
}
```

### 2.3 语法

#### **2.3.1 语法格式一：**无参，无返回值

```java
@Test
public void test1(){
    //未使用Lambda表达式
    Runnable r1 = new Runnable() {
        @Override
        public void run() {
            System.out.println("我爱北京天安门");
        }
    };

    r1.run();

    System.out.println("***********************");

    //使用Lambda表达式
    Runnable r2 = () -> {
        System.out.println("我爱北京故宫");
    };

    r2.run();
}
```



#### **2.3.2 语法格式二：**Lambda 需要一个参数，但是没有返回值。

```java
@Test
public void test2(){
    //未使用Lambda表达式
    Consumer<String> con = new Consumer<String>() {
        @Override
        public void accept(String s) {
            System.out.println(s);
        }
    };
    con.accept("谎言和誓言的区别是什么？");

    System.out.println("*******************");

    //使用Lambda表达式
    Consumer<String> con1 = (String s) -> {
        System.out.println(s);
    };
    con1.accept("一个是听得人当真了，一个是说的人当真了");

}
```



#### **2.3.3 语法格式三：**数据类型可以省略，因为可由编译器推断得出，称为“类型推断”

```java
@Test
public void test3(){
    //语法格式三使用前
    Consumer<String> con1 = (String s) -> {
        System.out.println(s);
    };
    con1.accept("一个是听得人当真了，一个是说的人当真了");

    System.out.println("*******************");
    //语法格式三使用后
    Consumer<String> con2 = (s) -> {
        System.out.println(s);
    };
    con2.accept("一个是听得人当真了，一个是说的人当真了");

}
```



#### **2.3.4 语法格式四：**Lambda 若只需要一个参数时，参数的小括号可以省略

```java
@Test
public void test4(){
    //语法格式四使用前
    Consumer<String> con1 = (s) -> {
        System.out.println(s);
    };
    con1.accept("一个是听得人当真了，一个是说的人当真了");

    System.out.println("*******************");
    //语法格式四使用后
    Consumer<String> con2 = s -> {
        System.out.println(s);
    };
    con2.accept("一个是听得人当真了，一个是说的人当真了");


}
```



#### **2.3.5 语法格式五：**Lambda 需要两个或以上的参数，多条执行语句，并且可以有返回值

```java
@Test
public void test5(){
    //语法格式五使用前
    Comparator<Integer> com1 = new Comparator<Integer>() {
        @Override
        public int compare(Integer o1, Integer o2) {
            System.out.println(o1);
            System.out.println(o2);
            return o1.compareTo(o2);
        }
    };

    System.out.println(com1.compare(12,21));
    System.out.println("*****************************");
    //语法格式五使用后
    Comparator<Integer> com2 = (o1,o2) -> {
        System.out.println(o1);
        System.out.println(o2);
        return o1.compareTo(o2);
    };

    System.out.println(com2.compare(12,6));


}
```



#### **2.3.6 语法格式六：**当 Lambda 体只有一条语句时，return 与大括号若有，都可以省略

```java
@Test
public void test6(){
    //语法格式六使用前
    Comparator<Integer> com1 = (o1,o2) -> {
        return o1.compareTo(o2);
    };

    System.out.println(com1.compare(12,6));

    System.out.println("*****************************");
    //语法格式六使用后
    Comparator<Integer> com2 = (o1,o2) -> o1.compareTo(o2);

    System.out.println(com2.compare(12,21));

}

@Test
public void test7(){
    //语法格式六使用前
    Consumer<String> con1 = s -> {
        System.out.println(s);
    };
    con1.accept("一个是听得人当真了，一个是说的人当真了");

    System.out.println("*****************************");
    //语法格式六使用后
    Consumer<String> con2 = s -> System.out.println(s);

    con2.accept("一个是听得人当真了，一个是说的人当真了");

}
```



## 3. Java8新特性：函数式(Functional)接口

### 3.1 什么是函数式接口

- 只包含`一个抽象方法`（Single Abstract Method，简称SAM）的接口，称为函数式接口。当然该接口可以包含其他非抽象方法。
- 你可以通过 Lambda 表达式来创建该接口的对象。（若 Lambda 表达式抛出一个受检异常(即：非运行时异常)，那么该异常需要在目标接口的抽象方法上进行声明）。
- 我们可以在一个接口上使用 `@FunctionalInterface` 注解，这样做可以检查它是否是一个函数式接口。同时 javadoc 也会包含一条声明，说明这个接口是一个函数式接口。
- 在`java.util.function`包下定义了Java 8 的丰富的函数式接口

### 3.2 如何理解函数式接口

- 面向对象的思想：
  - 做一件事情，找一个能解决这个事情的对象，调用对象的方法，完成事情。
- 函数式编程思想：
  - 只要能获取到结果，谁去做的，怎么做的都不重要，重视的是结果，不重视过程。
- 在函数式编程语言当中，函数被当做一等公民对待。在将函数作为一等公民的编程语言中，Lambda表达式的类型是函数。但是在Java8中，有所不同。在Java8中，Lambda表达式是对象，而不是函数，它们必须依附于一类特别的对象类型——函数式接口。
- 简单的说，在Java8中，Lambda表达式就是一个函数式接口的实例。这就是Lambda表达式和函数式接口的关系。也就是说，只要一个对象是函数式接口的实例，那么该对象就可以用Lambda表达式来表示。

### 3.3 举例

<img src="http://jason243.online/javase_songhongkang/images/image-20220527111621424.png" alt="image-20220527111621424" style="zoom:80%;" />

作为参数传递 Lambda 表达式：

<img src="http://jason243.online/javase_songhongkang/images/image-20220527111751485.png" alt="image-20220527111751485" style="zoom:80%;" />

> 作为参数传递 Lambda 表达式：为了将 Lambda 表达式作为参数传递，接收Lambda 表达式的参数类型必须是与该 Lambda 表达式兼容的函数式接口的类型。

### 3.4 Java 内置函数式接口

#### 3.4.1 之前的函数式接口

之前学过的接口，有些就是函数式接口，比如：

- java.lang.Runnable
  - public void run()
- java.lang.Iterable<T>
  - public Iterator<T> iterate()
- java.lang.Comparable<T>
  - public int compareTo(T t)
- java.util.Comparator<T>
  - public int compare(T t1, T t2)

#### 3.4.2 四大核心函数式接口

| 函数式接口         | 称谓       | 参数类型 | 用途                                                         |
| ------------------ | ---------- | -------- | ------------------------------------------------------------ |
| `Consumer<T>  `    | 消费型接口 | T        | 对类型为T的对象应用操作，包含方法：  `void accept(T t)  `    |
| `Supplier<T>  `    | 供给型接口 | 无       | 返回类型为T的对象，包含方法：`T get()  `                     |
| `Function<T, R>  ` | 函数型接口 | T        | 对类型为T的对象应用操作，并返回结果。结果是R类型的对象。包含方法：`R apply(T t)  ` |
| `Predicate<T>  `   | 判断型接口 | T        | 确定类型为T的对象是否满足某约束，并返回 boolean 值。包含方法：`boolean test(T t)  ` |

#### 3.4.3 其它接口

**类型1：消费型接口**

**类型2：供给型接口**

**类型3：函数型接口**

**类型4：判断型接口**

## 4. Java8新特性：方法引用与构造器引用

Lambda表达式是可以简化函数式接口的变量或形参赋值的语法。而方法引用和构造器引用是为了简化Lambda表达式的。

### 4.1 方法引用

当要传递给Lambda体的操作，已经有实现的方法了，可以使用方法引用！

方法引用可以看做是Lambda表达式深层次的表达。换句话说，方法引用就是Lambda表达式，也就是函数式接口的一个实例，通过方法的名字来指向一个方法，可以认为是Lambda表达式的一个语法糖。

> 语法糖（Syntactic sugar），也译为糖衣语法，是由英国计算机科学家彼得·约翰·兰达（Peter J. Landin）发明的一个术语，指计算机语言中添加的某种语法，这种语法`对语言的功能并没有影响，但是更方便程序员使用`。通常来说使用语法糖能够增加程序的可读性，从而减少程序代码出错的机会。

#### 4.1.1 方法引用格式

- 格式：使用方法引用操作符 “`::`” 将类(或对象) 与 方法名分隔开来。
  - 两个:中间不能有空格，而且必须英文状态下半角输入
- 如下三种主要使用情况：
  - 情况1：`对象 :: 实例方法名`
  - 情况2：`类 :: 静态方法名`
  - 情况3：`类 :: 实例方法名`

#### 4.1.2 方法引用使用前提

**要求1：**Lambda体只有一句语句，并且是通过调用一个对象的/类现有的方法来完成的

例如：System.out对象，调用println()方法来完成Lambda体

​           Math类，调用random()静态方法来完成Lambda体

**要求2：**

针对情况1：函数式接口中的抽象方法a在被重写时使用了某一个对象的方法b。如果方法a的形参列表、返回值类型与方法b的形参列表、返回值类型都相同，则我们可以使用方法b实现对方法a的重写、替换。

针对情况2：函数式接口中的抽象方法a在被重写时使用了某一个类的静态方法b。如果方法a的形参列表、返回值类型与方法b的形参列表、返回值类型都相同，则我们可以使用方法b实现对方法a的重写、替换。

针对情况3：函数式接口中的抽象方法a在被重写时使用了某一个对象的方法b。如果方法a的返回值类型与方法b的返回值类型相同，同时方法a的形参列表中有n个参数，方法b的形参列表有n-1个参数，且方法a的第1个参数作为方法b的调用者，且方法a的后n-1参数与方法b的n-1参数匹配（类型相同或满足多态场景也可以）

例如：t->System.out.println(t)

​        () -> Math.random() 都是无参

#### 4.1.3 举例

```java
public class MethodRefTest {

	// 情况一：对象 :: 实例方法
	//Consumer中的void accept(T t)
	//PrintStream中的void println(T t)
	@Test
	public void test1() {
		Consumer<String> con1 = str -> System.out.println(str);
		con1.accept("北京");

		System.out.println("*******************");
		PrintStream ps = System.out;
		Consumer<String> con2 = ps::println;
		con2.accept("beijing");
	}
	
	//Supplier中的T get()
	//Employee中的String getName()
	@Test
	public void test2() {
		Employee emp = new Employee(1001,"Tom",23,5600);

		Supplier<String> sup1 = () -> emp.getName();
		System.out.println(sup1.get());

		System.out.println("*******************");
		Supplier<String> sup2 = emp::getName;
		System.out.println(sup2.get());

	}

	// 情况二：类 :: 静态方法
	//Comparator中的int compare(T t1,T t2)
	//Integer中的int compare(T t1,T t2)
	@Test
	public void test3() {
		Comparator<Integer> com1 = (t1,t2) -> Integer.compare(t1,t2);
		System.out.println(com1.compare(12,21));

		System.out.println("*******************");

		Comparator<Integer> com2 = Integer::compare;
		System.out.println(com2.compare(12,3));

	}
	
	//Function中的R apply(T t)
	//Math中的Long round(Double d)
	@Test
	public void test4() {
		Function<Double,Long> func = new Function<Double, Long>() {
			@Override
			public Long apply(Double d) {
				return Math.round(d);
			}
		};

		System.out.println("*******************");

		Function<Double,Long> func1 = d -> Math.round(d);
		System.out.println(func1.apply(12.3));

		System.out.println("*******************");

		Function<Double,Long> func2 = Math::round;
		System.out.println(func2.apply(12.6));
	}

	// 情况三：类 :: 实例方法  (有难度)
	// Comparator中的int comapre(T t1,T t2)
	// String中的int t1.compareTo(t2)
	@Test
	public void test5() {
		Comparator<String> com1 = (s1,s2) -> s1.compareTo(s2);
		System.out.println(com1.compare("abc","abd"));

		System.out.println("*******************");

		Comparator<String> com2 = String :: compareTo;
		System.out.println(com2.compare("abd","abm"));
	}

	//BiPredicate中的boolean test(T t1, T t2);
	//String中的boolean t1.equals(t2)
	@Test
	public void test6() {
		BiPredicate<String,String> pre1 = (s1,s2) -> s1.equals(s2);
		System.out.println(pre1.test("abc","abc"));

		System.out.println("*******************");
		BiPredicate<String,String> pre2 = String :: equals;
		System.out.println(pre2.test("abc","abd"));
	}
	
	// Function中的R apply(T t)
	// Employee中的String getName();
	@Test
	public void test7() {
		Employee employee = new Employee(1001, "Jerry", 23, 6000);


		Function<Employee,String> func1 = e -> e.getName();
		System.out.println(func1.apply(employee));

		System.out.println("*******************");
		Function<Employee,String> func2 = Employee::getName;
		System.out.println(func2.apply(employee));
	}

}

```

### 4.2 构造器引用

当Lambda表达式是创建一个对象，并且满足Lambda表达式形参，正好是给创建这个对象的构造器的实参列表，就可以使用构造器引用。

格式：`类名::new`

举例：

```java
public class ConstructorRefTest {
	//构造器引用
    //Supplier中的T get()
    //Employee的空参构造器：Employee()
    @Test
    public void test1(){

        Supplier<Employee> sup = new Supplier<Employee>() {
            @Override
            public Employee get() {
                return new Employee();
            }
        };
        System.out.println("*******************");

        Supplier<Employee>  sup1 = () -> new Employee();
        System.out.println(sup1.get());

        System.out.println("*******************");

        Supplier<Employee>  sup2 = Employee :: new;
        System.out.println(sup2.get());
    }

	//Function中的R apply(T t)
    @Test
    public void test2(){
        Function<Integer,Employee> func1 = id -> new Employee(id);
        Employee employee = func1.apply(1001);
        System.out.println(employee);

        System.out.println("*******************");

        Function<Integer,Employee> func2 = Employee :: new;
        Employee employee1 = func2.apply(1002);
        System.out.println(employee1);

    }

	//BiFunction中的R apply(T t,U u)
    @Test
    public void test3(){
        BiFunction<Integer,String,Employee> func1 = (id,name) -> new Employee(id,name);
        System.out.println(func1.apply(1001,"Tom"));

        System.out.println("*******************");

        BiFunction<Integer,String,Employee> func2 = Employee :: new;
        System.out.println(func2.apply(1002,"Tom"));
    }
}
```

### 4.3 数组构造引用

当Lambda表达式是创建一个数组对象，并且满足Lambda表达式形参，正好是给创建这个数组对象的长度，就可以数组构造引用。

格式：`数组类型名::new`

举例：

```java
//数组引用
//Function中的R apply(T t)
@Test
public void test4(){
    Function<Integer,String[]> func1 = length -> new String[length];
    String[] arr1 = func1.apply(5);
    System.out.println(Arrays.toString(arr1));

    System.out.println("*******************");

    Function<Integer,String[]> func2 = String[] :: new;
    String[] arr2 = func2.apply(10);
    System.out.println(Arrays.toString(arr2));

}

```

## 5. Java8新特性：强大的Stream API

### 5.1 说明

- Java8中有两大最为重要的改变。第一个是 Lambda 表达式；另外一个则是 Stream API。
- Stream API ( java.util.stream) 把真正的函数式编程风格引入到Java中。这是目前为止对Java类库`最好的补充`，因为Stream API可以极大提供Java程序员的生产力，让程序员写出高效率、干净、简洁的代码。
- Stream 是 Java8 中处理集合的关键抽象概念，它可以指定你希望对集合进行的操作，可以执行非常复杂的查找、过滤和映射数据等操作。 **使用Stream API 对集合数据进行操作，就类似于使用 SQL 执行的数据库查询。**也可以使用 Stream API 来并行执行操作。简言之，Stream API 提供了一种高效且易于使用的处理数据的方式。

### 5.2 什么是Stream

Stream 是数据渠道，用于操作数据源（集合、数组等）所生成的元素序列。

Stream 和 Collection 集合的区别：**Collection 是一种静态的内存数据结构，讲的是数据，而 Stream 是有关计算的，讲的是计算。**

注意：

①Stream 自己不会存储元素。

②Stream 不会改变源对象。相反，他们会返回一个持有结果的新Stream。

③Stream 操作是延迟执行的。这意味着他们会等到需要结果的时候才执行。即一旦执行终止操作，就执行中间操作链，并产生结果。

④ Stream一旦执行了终止操作，就不能再调用其它中间操作或终止操作了。

### 5.3 Stream的操作三个步骤

**1- 创建 Stream**
一个数据源（如：集合、数组），获取一个流

**2- 中间操作**
每次处理都会返回一个持有结果的新Stream，即中间操作的方法返回值仍然是Stream类型的对象。因此中间操作可以是个`操作链`，可对数据源的数据进行n次处理，但是在终结操作前，并不会真正执行。

**3- 终止操作(终端操作)**
终止操作的方法返回值类型就不再是Stream了，因此一旦执行终止操作，就结束整个Stream操作了。一旦执行终止操作，就执行中间操作链，最终产生结果并结束Stream。

<img src="http://jason243.online/javase_songhongkang/images/image-20220514180803311.png" alt="image-20220514180803311" style="zoom: 50%;" />

#### 5.3.1 创建Stream实例

**方式一：通过集合**

Java8 中的 Collection 接口被扩展，提供了两个获取流的方法：

- default Stream<E> stream() : 返回一个顺序流
- default Stream<E> parallelStream() : 返回一个并行流

```java
@Test
public void test01(){
    List<Integer> list = Arrays.asList(1,2,3,4,5);

    //JDK1.8中，Collection系列集合增加了方法
    Stream<Integer> stream = list.stream();
}
```



**方式二：通过数组**

Java8 中的 Arrays 的静态方法 stream() 可以获取数组流：

- static <T> Stream<T> stream(T[] array): 返回一个流
- public static IntStream stream(int[] array)
- public static LongStream stream(long[] array)
- public static DoubleStream stream(double[] array)

```java
@Test
public void test02(){
    String[] arr = {"hello","world"};
    Stream<String> stream = Arrays.stream(arr); 
}

@Test
public void test03(){
    int[] arr = {1,2,3,4,5};
    IntStream stream = Arrays.stream(arr);
}
```



**方式三：通过Stream的of()**

可以调用Stream类静态方法 of(), 通过显示值创建一个流。它可以接收任意数量的参数。

- public static<T> Stream<T> of(T... values) : 返回一个流

```java
@Test
public void test04(){
    Stream<Integer> stream = Stream.of(1,2,3,4,5);
    stream.forEach(System.out::println);
}
```



**方式四：创建无限流(了解)**

可以使用静态方法 Stream.iterate() 和 Stream.generate(), 创建无限流。

- 迭代
  public static<T> Stream<T> iterate(final T seed, final UnaryOperator<T> f) 
- 生成
  public static<T> Stream<T> generate(Supplier<T> s) 

```java
// 方式四：创建无限流
@Test
public void test05() {
	// 迭代
	// public static<T> Stream<T> iterate(final T seed, final
	// UnaryOperator<T> f)
	Stream<Integer> stream = Stream.iterate(0, x -> x + 2);
	stream.limit(10).forEach(System.out::println);

	// 生成
	// public static<T> Stream<T> generate(Supplier<T> s)
	Stream<Double> stream1 = Stream.generate(Math::random);
	stream1.limit(10).forEach(System.out::println);
}
```

#### 5.4.2 一系列中间操作

多个中间操作可以连接起来形成一个流水线，除非流水线上触发终止操作，否则中间操作不会执行任何的处理！而在终止操作时一次性全部处理，称为“惰性求值”。

1-筛选与切片

| **方   法**             | **描   述**                                                  |
| ----------------------- | ------------------------------------------------------------ |
| **filter(Predicatep)**  | 接收  Lambda ， 从流中排除某些元素                           |
| **distinct()**          | 筛选，通过流所生成元素的  hashCode() 和 equals() 去除重复元素 |
| **limit(long maxSize)** | 截断流，使其元素不超过给定数量                               |
| **skip(long n)**        | 跳过元素，返回一个扔掉了前  n 个元素的流。<br>若流中元素不足 n 个，则返回一个空流。与 limit(n) 互补 |

2-映 射

| **方法**                            | **描述**                                                     |
| ----------------------------------- | ------------------------------------------------------------ |
| **map(Function f)**                 | 接收一个函数作为参数，该函数会被应用到每个元素上，并将其映射成一个新的元素。 |
| **mapToDouble(ToDoubleFunction f)** | 接收一个函数作为参数，该函数会被应用到每个元素上，产生一个新的 DoubleStream。 |
| **mapToInt(ToIntFunction  f)**      | 接收一个函数作为参数，该函数会被应用到每个元素上，产生一个新的  IntStream。 |
| **mapToLong(ToLongFunction  f)**    | 接收一个函数作为参数，该函数会被应用到每个元素上，产生一个新的  LongStream。 |
| **flatMap(Function  f)**            | 接收一个函数作为参数，将流中的每个值都换成另一个流，然后把所有流连接成一个流 |

3-排序

| **方法**                       | **描述**                           |
| ------------------------------ | ---------------------------------- |
| **sorted()**                   | 产生一个新流，其中按自然顺序排序   |
| **sorted(Comparator** **com)** | 产生一个新流，其中按比较器顺序排序 |

#### 5.4.3 终止操作

- 终端操作会从流的流水线生成结果。其结果可以是任何不是流的值，例如：List、Integer，甚至是 void 。
- 流进行了终止操作后，不能再次使用。

1-匹配与查找

| **方法**                        | **描述**                                                     |
| ------------------------------- | ------------------------------------------------------------ |
| **allMatch(Predicate  p)**      | 检查是否匹配所有元素                                         |
| **anyMatch(Predicate  p)  **    | 检查是否至少匹配一个元素                                     |
| **noneMatch(Predicate**  **p)** | 检查是否没有匹配所有元素                                     |
| **findFirst()**                 | 返回第一个元素                                               |
| **findAny()**                   | 返回当前流中的任意元素                                       |
| **count()**                     | 返回流中元素总数                                             |
| **max(Comparator c)**           | 返回流中最大值                                               |
| **min(Comparator c)**           | 返回流中最小值                                               |
| **forEach(Consumer c)**         | 内部迭代(使用  Collection  接口需要用户去做迭代，称为外部迭代。<br>相反，Stream  API 使用内部迭代——它帮你把迭代做了) |

2-归约

| **方法**                                  | **描述**                                                 |
| ----------------------------------------- | -------------------------------------------------------- |
| **reduce(T  identity, BinaryOperator b)** | 可以将流中元素反复结合起来，得到一个值。返回  T          |
| **reduce(BinaryOperator  b)**             | 可以将流中元素反复结合起来，得到一个值。返回 Optional<T> |

备注：map 和 reduce 的连接通常称为 map-reduce 模式，因 Google 用它来进行网络搜索而出名。

3-收集

| **方   法**               | **描   述**                                                  |
| ------------------------- | ------------------------------------------------------------ |
| **collect(Collector  c)** | 将流转换为其他形式。接收一个  Collector接口的实现，<br>用于给Stream中元素做汇总的方法 |

Collector 接口中方法的实现决定了如何对流执行收集的操作(如收集到 List、Set、Map)。

另外， Collectors 实用类提供了很多静态方法，可以方便地创建常见收集器实例，具体方法与实例如下表：

| **方法**   | **返回类型**             | **作用**             |
| ---------- | ------------------------ | -------------------- |
| **toList** | Collector<T, ?, List<T>> | 把流中元素收集到List |

```java
List<Employee> emps= list.stream().collect(Collectors.toList());

```

| **方法**  | **返回类型**            | **作用**            |
| --------- | ----------------------- | ------------------- |
| **toSet** | Collector<T, ?, Set<T>> | 把流中元素收集到Set |

```java
Set<Employee> emps= list.stream().collect(Collectors.toSet());

```

| **方法**         | **返回类型**       | **作用**                   |
| ---------------- | ------------------ | -------------------------- |
| **toCollection** | Collector<T, ?, C> | 把流中元素收集到创建的集合 |

```java
Collection<Employee> emps =list.stream().collect(Collectors.toCollection(ArrayList::new));

```

| **方法**     | **返回类型**          | **作用**           |
| ------------ | --------------------- | ------------------ |
| **counting** | Collector<T, ?, Long> | 计算流中元素的个数 |

```java
long count = list.stream().collect(Collectors.counting());

```

| **方法**       | **返回类型**             | **作用**                 |
| -------------- | ------------------------ | ------------------------ |
| **summingInt** | Collector<T, ?, Integer> | 对流中元素的整数属性求和 |

```java
int total=list.stream().collect(Collectors.summingInt(Employee::getSalary));

```

| **方法**         | **返回类型**            | **作用**                        |
| ---------------- | ----------------------- | ------------------------------- |
| **averagingInt** | Collector<T, ?, Double> | 计算流中元素Integer属性的平均值 |

```java
double avg = list.stream().collect(Collectors.averagingInt(Employee::getSalary));

```

| **方法**           | **返回类型**                          | **作用**                                |
| ------------------ | ------------------------------------- | --------------------------------------- |
| **summarizingInt** | Collector<T, ?, IntSummaryStatistics> | 收集流中Integer属性的统计值。如：平均值 |

```java
int SummaryStatisticsiss= list.stream().collect(Collectors.summarizingInt(Employee::getSalary));
```

| **方法**    | **返回类型**                       | **作用**           |
| ----------- | ---------------------------------- | ------------------ |
| **joining** | Collector<CharSequence, ?, String> | 连接流中每个字符串 |

```java
String str= list.stream().map(Employee::getName).collect(Collectors.joining());
```

| **方法**  | **返回类型**                 | **作用**             |
| --------- | ---------------------------- | -------------------- |
| **maxBy** | Collector<T, ?, Optional<T>> | 根据比较器选择最大值 |

```java
Optional<Emp>max= list.stream().collect(Collectors.maxBy(comparingInt(Employee::getSalary)));
```

| **方法**  | **返回类型**                 | **作用**             |
| --------- | ---------------------------- | -------------------- |
| **minBy** | Collector<T, ?, Optional<T>> | 根据比较器选择最小值 |

```java
Optional<Emp> min = list.stream().collect(Collectors.minBy(comparingInt(Employee::getSalary)));
```

| **方法**     | **返回类型**                 | **作用**                                                     |
| ------------ | ---------------------------- | ------------------------------------------------------------ |
| **reducing** | Collector<T, ?, Optional<T>> | 从一个作为累加器的初始值开始，利用BinaryOperator与流中元素逐个结合，从而归约成单个值 |

```java
int total=list.stream().collect(Collectors.reducing(0, Employee::getSalar, Integer::sum));
```

| **方法**              | **返回类型**      | **作用**                           |
| --------------------- | ----------------- | ---------------------------------- |
| **collectingAndThen** | Collector<T,A,RR> | 包裹另一个收集器，对其结果转换函数 |

```java
int how= list.stream().collect(Collectors.collectingAndThen(Collectors.toList(), List::size));
```

| **方法**       | **返回类型**                     | **作用**                               |
| -------------- | -------------------------------- | -------------------------------------- |
| **groupingBy** | Collector<T, ?, Map<K, List<T>>> | 根据某属性值对流分组，属性为K，结果为V |

```java
Map<Emp.Status, List<Emp>> map= list.stream().collect(Collectors.groupingBy(Employee::getStatus));
```

| **方法**           | **返回类型**                           | **作用**                |
| ------------------ | -------------------------------------- | ----------------------- |
| **partitioningBy** | Collector<T, ?, Map<Boolean, List<T>>> | 根据true或false进行分区 |

```java
Map<Boolean,List<Emp>> vd = list.stream().collect(Collectors.partitioningBy(Employee::getManage));
```

### 5.5 Java9新增API

**新增1：Stream实例化方法**

ofNullable()的使用：

Java 8 中 Stream 不能完全为null，否则会报空指针异常。而 Java 9 中的 ofNullable 方法允许我们创建一个单元素 Stream，可以包含一个非空元素，也可以创建一个空 Stream。

```java
//报NullPointerException
//Stream<Object> stream1 = Stream.of(null);
//System.out.println(stream1.count());

//不报异常，允许通过
Stream<String> stringStream = Stream.of("AA", "BB", null);
System.out.println(stringStream.count());//3

//不报异常，允许通过
List<String> list = new ArrayList<>();
list.add("AA");
list.add(null);
System.out.println(list.stream().count());//2
//ofNullable()：允许值为null
Stream<Object> stream1 = Stream.ofNullable(null);
System.out.println(stream1.count());//0

Stream<String> stream = Stream.ofNullable("hello world");
System.out.println(stream.count());//1
```

iterator()重载的使用：

```java
//原来的控制终止方式：
Stream.iterate(1,i -> i + 1).limit(10).forEach(System.out::println);

//现在的终止方式：
Stream.iterate(1,i -> i < 100,i -> i + 1).forEach(System.out::println);
```



## 6、try - catch新特性（JDK9）

**JDK9的新特性**

try的前面可以定义流对象，try后面的()中可以直接引用流对象的名称。在try代码执行完毕后，流对象也可以释放掉，也不用写finally了。

格式：

```java
A a = new A();
B b = new B();
try(a;b){
    可能产生的异常代码
}catch(异常类名 变量名){
    异常处理的逻辑
}
```

举例：

```java
@Test
public void test04() {
    InputStreamReader reader = new InputStreamReader(System.in);
    OutputStreamWriter writer = new OutputStreamWriter(System.out);
    try (reader; writer) {
        //reader是final的，不可再被赋值
        //   reader = null;

    } catch (IOException e) {
        e.printStackTrace();
    }
}
```



## 7、instanceof新特性（JDK16）

instanceof的模式匹配

**JDK14中预览特性：**

instanceof 模式匹配通过提供更为简便的语法，来提高生产力。有了该功能，可以减少Java程序中显式强制转换的数量，实现更精确、简洁的类型安全的代码。

Java 14之前旧写法：

```java
if(obj instanceof String){
    String str = (String)obj; //需要强转
    .. str.contains(..)..
}else{
    ...
}
```

Java 14新特性写法：

```java
if(obj instanceof String str){
    .. str.contains(..)..
}else{
    ...
}
```

JDK16转正



## 8、文本块 `"""  """`（JDK13）

**JDK13的新特性**

使用"""作为文本块的开始符和结束符，在其中就可以放置多行的字符串，不需要进行任何转义。因此，文本块将提高Java程序的可读性和可写性。

基本使用：

```java
"""
line1
line2
line3
"""
```

相当于：

```java
"line1\nline2\nline3\n"
```

或者一个连接的字符串：

```java
"line1\n" +
"line2\n" +
"line3\n"
```

如果字符串末尾不需要行终止符，则结束分隔符可以放在最后一行内容上。例如：

```java
"""
line1
line2
line3"""
```

相当于

```java
"line1\nline2\nline3"
```



## 9、Record（JDK16）

> 觉得Java中写基本类太麻烦了，都是重复的工作，所以添加了Record类，类似官方Lombok，但是似乎被诟病并不好用

**JDK14中预览特性：神说要用record，于是就有了。**实现一个简单的数据载体类，为了避免编写：构造函数，访问器，equals()，hashCode () ，toString ()等，Java 14推出record。

`record` 是一种全新的类型，它本质上是一个 `final` 类，同时所有的属性都是 `final` 修饰，它会自动编译出 `public get` 、`hashcode` 、`equals`、`toString`、构造器等结构，减少了代码编写量。

具体来说：当你用`record` 声明一个类时，该类将自动拥有以下功能：

- 获取成员变量的简单方法，比如例题中的 name() 和 partner() 。注意区别于我们平常getter()的写法。
- 一个 equals 方法的实现，执行比较时会比较该类的所有成员属性。
- 重写 hashCode() 方法。
- 一个可以打印该类所有成员属性的 toString() 方法。
- 只有一个构造方法。

此外：

- 还可以在record声明的类中定义静态字段、静态方法、构造器或实例方法。
- 不能在record声明的类中定义实例字段；类不能声明为abstract；不能声明显式的父类等。

举例1（旧写法）：

```java
class Point {
    private final int x;
    private final int y;

    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    int x() {
        return x;
    }

    int y() {
        return y;
    }

    public boolean equals(Object o) {
        if (!(o instanceof Point)) return false;
        Point other = (Point) o;
        return other.x == x && other.y == y;
    }

    public int hashCode() {
        return Objects.hash(x, y);
    }

    @Override
    public String toString() {
        return "Point{" +
                "x=" + x +
                ", y=" + y +
                '}';
    }
}
```

举例1（新写法）：

```java
record Point(int x, int y) { }
```



## 10、密封类（JDK17）

> 让类可以指定哪些类能继承自己

背景：

在 Java 中如果想让一个类不能被继承和修改，这时我们应该使用 `final` 关键字对类进行修饰。不过这种要么可以继承，要么不能继承的机制不够灵活，有些时候我们可能想让某个类可以被某些类型继承，但是又不能随意继承，是做不到的。Java 15 尝试解决这个问题，引入了 `sealed` 类，被 `sealed` 修饰的类可以指定子类。这样这个类就只能被指定的类继承。

**JDK15的预览特性：**

通过密封的类和接口来限制超类的使用，密封的类和接口限制其它可能继承或实现它们的其它类或接口。

具体使用：

- 使用修饰符`sealed`，可以将一个类声明为密封类。密封的类使用保留关键字`permits`列出可以直接扩展（即extends）它的类。

- `sealed` 修饰的类的机制具有传递性，它的子类必须使用指定的关键字进行修饰，且只能是 `final`、`sealed`、`non-sealed` 三者之一。

举例：

```java
package com.atguigu.java;
public abstract sealed class Shape permits Circle, Rectangle, Square {...}

public final class Circle extends Shape {...} //final表示Circle不能再被继承了

public sealed class Rectangle extends Shape permits TransparentRectangle, FilledRectangle {...}

public final class TransparentRectangle extends Rectangle {...}

public final class FilledRectangle extends Rectangle {...}

public non-sealed class Square extends Shape {...} //non-sealed表示可以允许任何类继承
```

**JDK16二次预览特性**

**JDK17中转正特性**

