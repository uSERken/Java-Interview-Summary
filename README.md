# Java 面试题汇总及解答

让天下没有难拿的 Offer。欢迎在 Issue 中提出你遇到的或想得到解答的面试问题，或者你觉得某个某个问题有更好的解答，也欢迎 PR & Issue。

持续更新中...

## 基础篇

### 基本功

- 面向对象的特征
   - 封装
   - 继承
   - 多态


- final, finally, finalize 的区别
  - final 
      - final 修饰类,表示该类不可以被继承
      - final 修饰变量,分两种情况,如果修饰的是基本类型变量,那么只能被赋值一次,不能被赋值两次,
       如果修饰的是引用类型变量,那么引用指向的内存地址将不可变,但是引用类型内的属性可以被修改
      - final 修饰方法,表示该方法不可以被子类重写,但是可以被子类继承使用
   - finally 
      - finally 跟随 `try{}` 代码块,`try{}finally{}`
      - finally 跟随 `try{}catch{}` 代码块, `try{}catch{}finally{}`,
      一般情况都是在`finally`代码块
      写释放资源类代码,例如 数据库连接,流的关闭等,保证代码始终会被执行到
      - finally 的执行需要注意,只有当代码执行到`try`代码块的时候,`finally`才会执行,如果`try{}catch{}`内部都有
      return 语句,那么最终返回的结果,将是`finally` return的结果,
   - finalize 的使用跟作用
      - finalize 是顶级父类 `Object` 内的方法,所有子类都会继承该方法
      - finalize 方法,当JVM发现这个特定实例应该被垃圾收集时，会调用`finalize`方法,这样在该方法内可以做任何操作,例如阻止被垃圾回收等
      - finalize 的调用,是JVM触发调用,不是自己调用


 - int 和 Integer 有什么区别
   - int 是JAVA八个基本类型中的一个,它的值范围为 `2147483648～2147483647`,占用4个字节,32位
   - Integer 是引用类型,包装了基本类型中的`int`
   - int的初始化可以是 `int a = 1`,而 `Integer`的初始化可以是 `Integer a = 1` 或者 `Integer a = new Integer(1)`
   - Integer 缓存了 `-128~127` 范围数值在内部的一个数组内,该数值范围可以通过启动虚拟机参数 `-XX:AutoBoxCacheMax=` 进行设置大小
   并且在该范围内用==比较另外一个Integer的时候,实际上是int类型的比较,不过不推荐该方式,包装类型尽量使用`equals`来进行比较

 - 重载和重写的区别
   - 重载 
      - 重载是在编译的时候就确定执行哪个方法
      - 重载的签名,只有参数类型,参数个数,参数顺序参与签名,返回值不参与签名
      - 在同一个类中,如果方法名称一致,但是 参数个数,参数类型,参数顺序不一致,称之为重载,其中 `参数个数>参数类型>参数顺序,如果参数类型都一致`,
      但是顺序不同,是不算重载的
   - 重写
      - 重写存在子类继承父类中,其中子类定义一个方法,该方法的方法名,参数,类型都跟父类一致,称之为重写
      - 重写是多态的表现形式之一,重写的方法,只有在运行的时候,才能确定具体调用的是父类的方法还是子类的方法
      

 - 抽象类和接口有什么区别
   - 抽象类
      - 抽象类可以没有抽象方法,但是有抽象方法的类一定是抽象类
      - 一个类只能继承一个类,也就是只能继承一个抽象类
      - 抽象类内部,可以有抽象方法,也可以没有抽象方法,如果是抽象方法,那么如果子类不是抽象类,那么必须实现抽象方法
      - 抽象类不可以被直接实例化,它只是对一个事物的抽象,只能被声明,不能被实例化
      - 抽象类内 属性跟方法默认的访问权限都是 `protected`
      - 抽象类内部可以定义 `private`的属性跟方法
      - 定义抽象类是使用在类名前加入 `abstract`
   - 接口
      - 接口是一系列方法的申明,JDK1.8之前接口内只有方法声明,没有方法的实现,JDK1.8后,接口可以定义默认的实现
      - 接口只负责定义方法,具体的实现,将有子类去实现
      - 接口所有方法,默认的访问权限都是 `public`
      - 接口不能被直接实例化,因为它也是对一个事物的抽象,只能申明,不能被实例化
      - 一个类可以实现多个接口
      - 接口内部不能定义 `private`的方法,因为私有方法没有实现是没有意义的
      - 定义接口是使用 `interface`


 - 说说反射的用途及实现



 - 说说自定义注解的场景及实现



 - HTTP 请求的 GET 与 POST 方式的区别



 - session 与 cookie 区别



 - session 分布式处理



 - JDBC 流程



 - MVC 设计思想



 - equals 与 == 的区别

   - 要理解 `equals` 跟`==` 的区别,首先我们要知道java里面只有基本类型跟引用类型,基本类型存储在`栈`中,而引用类型存储在`堆`内

   - `==`既可以用于基本类型的比较,也可以用于引用类型的比较,但是两者用`==`比较是有不同的

     -  `==`比较基本类型的时候,比较的是值大小例如: 

       ```java
       //基本类型用 == 比较,其实比较的是 值
       int a = 1;
       int b = 1;
       //打印结果为 true 因为 1==1 是真
       System.out.println(a == b);      

       //引用类型使用==比较,比较的实际上是在堆内的内存地址,例如:
       User u1 = new User();
       User u2 = new User();
       //打印结果为 false 因为两个对象的内存地址不相等
       System.out.println(u1==u2);

       ```

     ​

     - 所以基本类型用`==`比较是没有问题的,但是引用类型却不能使用`==`比较,因为两个引用类型在内存中的地址是不一样的,用`==`比较两个引用类型会得到false
     - String最好也不好用`==`比较,虽然常量池内会预先保留一些字符串,但是避免万一,String最好还是用`equals`来进行比较

     ​

   - `euqals`只能用于比较引用类型,它是超类`Object`的方法,默认的实现是`==`比较,也就是`默认比较两个引用对象的内存地址值`,所以我们要判断两个引用类型是否相等,不能通过内存地址去比较,一般是通过引用类型内部的属性的比较,来判断两个引用类型是否相等,例如:

     > 有个User对象,内部定义了 name,age,id 三个属性,我们可以认为,只要这三个属性相等,就是同一个对象,这时候我们就可以重写`equals`方法来判断,毕竟,OOP的面向对象,就是对现实世界的抽象嘛..

   ​

   - 总结  

     - `==` 在用于基本类型比较的时候,比较的是基本类型的值是否相等
     - `==` 在用于引用类型比较的时候,比较的是内存地址是否相同
     - `equals`在引用类型重写了`Object`方法的时候比较的是自己定义的比较方式,如果没有重写该方法,那么默认使用的是`==`比较,也就是比较两个对象的内存地址

     ​



### 集合

- List 和 Set 区别
- List 和 Map 区别
- Arraylist 与 LinkedList 区别
- ArrayList 与 Vector 区别
- HashMap 和 Hashtable 的区别
- HashSet 和 HashMap 区别
- HashMap 和 ConcurrentHashMap 的区别
- HashMap 的工作原理及代码实现
- ConcurrentHashMap 的工作原理及代码实现

### 线程

- 创建线程的方式及实现

只有一种创建线程的方式：new Thread()；Executors,ThreadPoolExecutor 等线程池做了线程的管理和复用，但最终依旧是通过 new Thread() 来创建线程；Runnable，Callable 创建的是任务，最终需要依托于线程去运行，和线程有本质的区别。

- sleep() 、join() 、yield() 有什么区别

sleep() 常用于让线程当前线程睡眠一段时间之后再执行。running -> blocked
join() 常用于控制多个线程的执行次序,例如可以将两个交替执行的线程调度为顺序执行.比如在B线程中调用A线程的 join() 方法,直到A线程执行完毕,B线程才会继续执行.在B线程中表现为 running -> blocked
yield() 不常用，作用于当前线程，手动控制当前线程让出线程调度器的时间片，但又可能刚刚让出，又立刻抢到时间片，继续执行。running -> runnable

- 说说 CountDownLatch 原理
- 说说 CyclicBarrier 原理
- 说说 Semaphore 原理
- 说说 Exchanger 原理
- 说说 CountDownLatch 与 CyclicBarrier 区别
- ThreadLocal 原理分析

ThreadLocal 常用于维护线程私有化变量，解决线程安全问题。其内部维护了一个 ThreadLocalMap，使用 Thread 作为 key，ThreadLocal.set 的值作为 value。并且和 HashMap 使用链表+红黑树解决 Hash 冲突不同（拉链法），它使用线性探测法解决 Hash 冲突，并且 Entry 是软引用，方便不再使用时自动触发回收。

- 讲讲线程池的实现原理
- 线程池的几种方式
- 线程的生命周期

Thread 被创建后处于新建状态(New)，当线程调用了 start() 方法后，进入了就绪状态(Runnable)，但 CPU 不一定为其立刻分配时间片，等待真正分配时间片(这完全取决于 CPU 的行为，程序无法控制)，线程进入运行状态(Running)，处于运行状态的线程可能由于 CPU 的调度行为让出时间片，重新进入就绪状态(Runnable)，也有可能会由于 sleep，阻塞 IO，锁等行为的影响进入阻塞状态，此时他们依旧持有 CPU 的时间片，当运行状态结束，线程进入死亡状态(Dead)。

### 锁机制

- 说说线程安全问题

多线程在并发访问共享资源时会存在线程安全问题；当多个线程访问一个对象时，如果不用考虑这些线程在运行时环境下的调度和交替执行，也不需要进行额外的同步，或者在调度方进行任何其他的协调操作，调用这个对象的行为都可以获得正确的结果，那么这个对象就是线程安全的 。

- 说说对 volatile 的理解

volatile 具有两大特性：禁止重排序、内存可见性。常用于单例模式中修饰单例变量，防止指令重排序；修饰成员变量，使得多线程并发操作下的共享变量在各个线程间互相可见。

详细介绍：https://www.jianshu.com/p/506c1e38a922

- 说说对 synchronized 的理解

Java 中的同步关键字，可以修饰方法，代码块，synchronized 可以保证方法或者代码块在运行时，同一时刻只有一个方法可以进入到临界区，同时它还可以保证共享变量的内存可见性。使用 synchronized 同步时需要做到尽量锁住尽量小的代码。

扩展：分布式场景下需要使用分布式锁。

- synchronized 与 Lock 的对比

两者都是重入锁，可以保证代码的同步，Lock 相对而言具备一些高级特性，如加锁的灵活度，更加丰富的 API，Lock 可以控制锁的公平性，以及具备读写锁等实现。

- 说说对 CAS 的理解

相对于对于`synchronized`这种阻塞加锁保证同步，CAS 使用非阻塞无锁算法保证了同步特性，其底层。如 Atomic* 类的底层实现以及 jdk1.8 的 ConcurrentHashMap 均使用到了 CAS 。其底层使用 unsafe.compareAndSwap 这样的 JNI 方法，调用 CPU 的 CAS 指令。

- ABA 问题以及业务上如何避免

线程 one 从内存位置 V 中取出 A，这时候另一个线程 two 也从内存中取出 A，并且 two 进行了一些操作变成了 B，然后 two 又将 V 位置的数据变成 A，这时候线程 one 进行 CAS 操作发现内存中仍然是 A，然后 one 操作成功。  尽管线程 one 的 CAS 操作成功，但是不代表这个过程就是没有问题的。 

如何避免：使用时间戳或者递增的 version 字段

- 乐观锁的业务场景及实现方式

乐观锁常用于可能会出现并发，但并发冲突不是特别激烈的场景。如将数据保存到数据库这样的操作，可以记录 version 或者时间戳这样的参数，在保存前与最新的值进行对比。

详细介绍：[使用JPA实现乐观锁](https://www.cnkirito.moe/jpa-OptimisticLock/)

## 核心篇

### 数据存储

- MySQL 索引使用的注意事项

  [参考](https://www.cnblogs.com/heyonggang/p/6610526.html)


- 说说反模式设计

反模式是指在对经常面对的问题经常使用的低效，不良，或者有待优化的设计模式/方法。甚至，反模式也可以是一种错误的开发思想/理念。在这里我举一个最简单的例子：在面向对象设计/编程中，有一条很重要的原则， 单一责任原则(Single responsibility principle)。其中心思想就是对于一个模块，或者一个类来说，这个模块或者这个类应该只对系统/软件的一个功能负责，而且该责任应该被该类完全封装起来。当开发人员需要修改系统的某个功能，这个模块/类是最主要的修改地方。相对应的一个反模式就是上帝类(God Class)，通常来说，这个类里面控制了很多其他的类，同时也依赖其他很多类。整个类不光负责自己的主要单一功能，而且还负责了其他很多功能，包括一些辅助功能。很多维护老程序的开发人员们可能都遇过这种类，一个类里有几千行的代码，有很多功能，但是责任不明确单一。单元测试程序也变复杂无比。维护/修改这个类的时间要远远超出其他类的时间。很多时候，形成这种情况并不是开发人员故意的。很多情况下主要是由于随着系统的年限，需求的变化，项目的资源压力，项目组人员流动，系统结构的变化而导致某些原先小型的，符合单一原则类慢慢的变的臃肿起来。最后当这个类变成了维护的噩梦(特别是原先熟悉的开发人员离职后)，重构该类就变成了一个不容易的工程。
[参考](http://blog.jobbole.com/87413)

- 说说分库与分表设计


[参考](https://infoq.cn/article/key-steps-and-likely-problems-of-split-table)

- 分库与分表带来的分布式困境与应对之策

[参考](https://juejin.im/entry/591968f6a0bb9f005ff7af23)


- 说说 SQL 优化之道

[参考1](https://cloud.tencent.com/developer/article/1054203)

[参考2](https://www.cnblogs.com/ggjucheng/archive/2012/11/11/2765465.html)

[参考3](https://hhbbz.github.io/2017/11/25/Mysql%E7%B4%A2%E5%BC%95%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9%E4%BB%A5%E5%8F%8A%E5%85%B3%E9%94%AE%E5%AD%97%E4%BC%98%E5%8C%96)


- MySQL 遇到的死锁问题

[参考](https://www.cnblogs.com/LBSer/p/5183300.htm)
- 存储引擎的 InnoDB 与 MyISAM
- 数据库索引的原理 为什么要用 B-tree

[参考](https://blog.csdn.net/kennyrose/article/details/7532032)


- 聚集索引与非聚集索引的区别
[参考](https://www.cnblogs.com/aspnethot/articles/1504082.html)

- limit 20000 加载很慢怎么解决

[参考](http://ourmysql.com/archives/1451)
- 选择合适的分布式主键方案

[参考1](https://juejin.im/post/5bb0217ef265da0ac2567b42)

[参考2](https://my.oschina.net/dolphinboy/blog/864567)


- 选择合适的数据存储方案
[参考](https://juejin.im/entry/58063fa1a0bb9f00589bab86)

- ObjectId 规则


- 聊聊 MongoDB 使用场景

[参考](https://www.zhihu.com/question/32071167)


- 倒排索引
[参考](http://www.cnblogs.com/zlslch/p/6440114.html

- 聊聊 ElasticSearch 使用场景

[参考](https://my.oschina.net/90888/blog/1619325)

### 缓存使用

- Redis 有哪些类型
[参考](http://www.runoob.com/redis/redis-data-types.html)

- Redis 内部结构

[参考](https://www.cnblogs.com/chenpingzhao/p/6965164.html)
- 聊聊 Redis 使用场景
[参考](https://juejin.im/post/5a24c6f2f265da431d3c8204)

- Redis 持久化机制
[参考](https://blog.csdn.net/u011784767/article/details/76824822)

- Redis 如何实现持久 [参考1](https://blog.csdn.net/u013905744/article/details/52787413) [参考2](https://www.jianshu.com/p/bedec93e5a7b)
- Redis 集群方案与实现 [参考](https://juejin.im/post/5a707f4d5188255a8817f5b1)[参考2](https://www.jianshu.com/p/14835303b07e)
- Redis 为什么是单线程的 [参考](https://blog.csdn.net/xlgen157387/article/details/79470556)             
- 缓存奔溃 - 缓存降级 - 使用缓存的合理性问题 [参考](https://blog.csdn.net/xlgen157387/article/details/79530877)

### 消息队列
[参考](https://www.swapassn.com/article/57)
- 消息队列的使用场景[参考](https://juejin.im/post/5add63c951882567183eb956)
- 消息的重发补偿解决思路
- 消息的幂等性解决思路
- 消息的堆积解决思路
- 自己如何实现消息队列
- 如何保证消息的有序性

## 框架篇

### Spring

- BeanFactory 和 ApplicationContext 有什么区别 [参考](https://blog.csdn.net/hi_kevin/article/details/7325554)
- Spring Bean 的生命周期 [参考](https://www.cnblogs.com/zrtqsk/p/3735273.html)
- Spring IOC 如何实现 [参考](https://www.jianshu.com/p/9fe5a3c25ab6)[参考](https://mp.weixin.qq.com/s?__biz=MzI4Njg5MDA5NA==&mid=2247484247&idx=1&sn=e228e29e344559e469ac3ecfa9715217&chksm=ebd74256dca0cb40059f3f627fc9450f916c1e1b39ba741842d91774f5bb7f518063e5acf5a0#rd)
- 说说 Spring AO  - Spring AOP 实现原理  [参考](https://juejin.im/post/5b06bf2df265da0de2574ee1)
- 动态代理（cglib 与 JDK）[参考](https://mp.weixin.qq.com/s?__biz=MzI4Njg5MDA5NA==&mid=2247484222&idx=1&sn=5191aca33f7b331adaef11c5e07df468&chksm=ebd7423fdca0cb29cdc59b4c79afcda9a44b9206806d2212a1b807c9f5879674934c37c250a1&scene=21#wechat_redirect)
- Spring 事务实现方式  - Spring 事务底层原理 [参考](https://juejin.im/post/5b00c52ef265da0b9527609)
- 如何自定义注解实现功能[参考](https://juejin.im/entry/57e496fd7db2a20063a24a3a)
- Spring MVC 运行流程
- Spring MVC 启动流程
- Spring 的单例实现原理
- Spring 框架中用到了哪些设计模式
- Spring 其他产品（Srping Boot、Spring Cloud、Spring Secuirity、Spring Data、Spring AMQP 等）

### Netty

- 为什么选择 Netty
- 说说业务中，Netty 的使用场景
- 原生的 NIO 在 JDK 1.7 版本存在 epoll bug
- 什么是TCP 粘包/拆包
- TCP粘包/拆包的解决办法
- Netty 线程模型
- 说说 Netty 的零拷贝
- Netty 内部执行流程
- Netty 重连实现

## 微服务篇

### 微服务

- 前后端分离是如何做的
- 微服务哪些框架
- 你怎么理解 RPC 框架
- 说说 RPC 的实现原理
- 说说 Dubbo 的实现原理
- 你怎么理解 RESTful
- 说说如何设计一个良好的 API
- 如何理解 RESTful API 的幂等性
- 如何保证接口的幂等性
- 说说 CAP 定理、 BASE 理论
- 怎么考虑数据一致性问题
- 说说最终一致性的实现方案
- 你怎么看待微服务
- 微服务与 SOA 的区别
- 如何拆分服务
- 微服务如何进行数据库管理
- 如何应对微服务的链式调用异常
- 对于快速追踪与定位问题
- 微服务的安全

### 分布式

- 谈谈业务中使用分布式的场景
- Session 分布式方案
- 分布式锁的场景
- 分布是锁的实现方案
- 分布式事务
- 集群与负载均衡的算法与实现
- 说说分库与分表设计
- 分库与分表带来的分布式困境与应对之策

## 安全&性能

### 安全问题

- 安全要素与 STRIDE 威胁
- 防范常见的 Web 攻击
- 服务端通信安全攻防
- HTTPS 原理剖析
- HTTPS 降级攻击
- 授权与认证
- 基于角色的访问控制
- 基于数据的访问控制

### 性能优化

- 性能指标有哪些
- 如何发现性能瓶颈
- 性能调优的常见手段
- 说说你在项目中如何进行性能调优

## 工程篇

### 需求分析

- 你如何对需求原型进行理解和拆分
- 说说你对功能性需求的理解
- 说说你对非功能性需求的理解
- 你针对产品提出哪些交互和改进意见
- 你如何理解用户痛点

### 设计能力

- 说说你在项目中使用过的 UML 图
- 你如何考虑组件化
- 你如何考虑服务化
- 你如何进行领域建模
- 你如何划分领域边界
- 说说你项目中的领域建模
- 说说概要设计

### 设计模式

- 你项目中有使用哪些设计模式
- 说说常用开源框架中设计模式使用分析
- 说说你对设计原则的理解
- 23种设计模式的设计理念
- 设计模式之间的异同，例如策略模式与状态模式的区别
- 设计模式之间的结合，例如策略模式+简单工厂模式的实践
- 设计模式的性能，例如单例模式哪种性能更好。

### 业务工程

- 你系统中的前后端分离是如何做的
- 说说你的开发流程
- 你和团队是如何沟通的
- 你如何进行代码评审
- 说说你对技术与业务的理解
- 说说你在项目中经常遇到的 Exception
- 说说你在项目中遇到感觉最难Bug，怎么解决的
- 说说你在项目中遇到印象最深困难，怎么解决的
- 你觉得你们项目还有哪些不足的地方
- 你是否遇到过 CPU 100% ，如何排查与解决
- 你是否遇到过 内存 OOM ，如何排查与解决
- 说说你对敏捷开发的实践
- 说说你对开发运维的实践
- 介绍下工作中的一个对自己最有价值的项目，以及在这个过程中的角色

### 软实力

- 说说你的亮点
- 说说你最近在看什么书
- 说说你觉得最有意义的技术书籍
- 工作之余做什么事情
- 说说个人发展方向方面的思考
- 说说你认为的服务端开发工程师应该具备哪些能力
- 说说你认为的架构师是什么样的，架构师主要做什么
- 说说你所理解的技术专家

## HR 篇

- 你为什么离开之前的公司
- 你为什么要进我们公司
- 说说职业规划
- 你如何看待加班问题
- 谈一谈你的一次失败经历
- 你觉得你最大的优点是什么
- 你觉得你最大的缺点是什么
- 你在工作之余做什么事情
- 你为什么认为你适合这个职位
- 你觉得自己那方面能力最急需提高
- 你来我们公司最希望得到什么
- 你希望从这份工作中获得什么
- 你对现在应聘的职位有什么了解
- 您还有什么想问的
- 你怎么看待自己的职涯
- 谈谈你的家庭情况
- 你有什么业余爱好
- 你计划在公司工作多久
