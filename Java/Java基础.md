### == 和 equals 的区别

- == 是用来判断对象的内存地址是否相等；基本数据类型使用  == 对比的是**值**，引用数据类型使用 == 对比的是**内存地址**。
- equals   本质上就是 ==，只不过 String 和 Integer 等重写了 equals 方法，把它变成了**值**比较 。

### 关键字 final

-  final 关键字可以用在三个地方：变量、方法、类。 

- final 修饰的类叫做最终类，能被继承 。
- final 修饰的方法不能被重写。 
- final 修饰的变量叫常量，常量必须初始化，初始化之后值就不能被修改。 

### 接口和抽象类

-  普通类不能包含抽象方法，抽象类可以包含抽象方法。 
-  抽象类是不能被实例化的，就是不能用new调出构造方法创建对象，普通类可以直接实例化。 
-  如果一个类继承于抽象类，则该子类必须实现父类的抽象方法。如果子类没有实现父类的抽象方法，则必须将子类也定义为abstract类。 
- 一个类可以实现多个接口，但只能实现一个抽象类。接口自己本身可以通过 extends 关键字扩展多个接口。
- 接口中除了 static、final 变量，不能有其他变量，而抽象类中则不一定。
- 从设计层面来说，抽象是对类的抽象，是一种模板设计，而接口是对行为的抽象，是一种行为的规范。

### Java的IO流

-  按功能来分：输入流（input）、输出流（output）。 

-  按类型来分：字节流和字符流。 

-  字节流和字符流的区别是：字节流按 8 位传输以字节为单位输入输出数据，字符流按 16 位传输以字符为单位输入输出数据。 

  ####  BIO、NIO、AIO ：

  -  BIO：Block IO 同步阻塞式 IO，就是我们平常使用的传统 IO，它的特点是模式简单使用方便，并发处理能力低。 

  -  NIO：New IO 同步非阻塞 IO，是传统 IO 的升级，客户端和服务器端通过 Channel（通道）通讯，实现了多路复用。 

  -  AIO：Asynchronous IO 是 NIO 的升级，也叫 NIO2，实现了异步非堵塞 IO ，异步 IO 的操作基于事件和回调机制。

     

### 操作字符串的类

-   Java 中操作字符串的类有 String 、 StringBuffer 、 StringBuilder 。
-   String 声明的是不可变的对象，每次操作都会生成新的 String 对象 。
-   StringBuffer和StringBuilder继承抽象类AbstractStringBuilder 。
-  StringBuffer、StringBuilder 存储数据的字符数组没有被final修饰，说明值可以改变，抽象类AbstractStringBuilder内部都提供了一个自动扩容机制，当发现长度不够的时候(初始默认长度是16)，会自动进行扩容工作 。 所以对于拼接字符串效率要比String要高。 
-  线程安全性 ： :StringBuilder > StringBuffer > String（ 多线程访问时，加锁和释放锁的过程很平凡，所以效率相比StringBuilder要低。StringBuilder相反执行效率高，但是线程不安全。所以单线程环境下推荐使用 StringBuilder，多线程环境下推荐使用 StringBuffer ）。 

### 参考来源

[面试整理]( https://www.cnblogs.com/Zz-maker/p/11193930.html )

[JavaGuide]( [https://snailclimb.gitee.io/javaguide/#/docs/java/Java%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86?id=_26-%e4%b8%8e-equals%e9%87%8d%e8%a6%81](https://snailclimb.gitee.io/javaguide/#/docs/java/Java基础知识?id=_26-与-equals重要) )