# JVM相关技术介绍

by Zhangchunxin

---

## JVM

Java Virtual Machine、Java虚拟机
<!-- .element: style="font-size: 24px;"--> 

它是整个Java实现跨平台的最核心的部分。
<!-- .element: class="fragment visible"--> 

--

### 操作系统中的位置

![](https://pic2.zhimg.com/80/v2-cfa3a5c9d1e3dc94b90384d75e625371_720w.jpg)

JVM就是运行在操作系统之上的一个软件。
<!-- .element: class="fragment visible"--> 

--

### JVM和JRE (Java Runtime Environment)

![](https://beginnersbook.com/wp-content/uploads/2013/05/jre.jpg)

JRE是运行基于Java语言编写的程序所不可缺少的运行环境，包括JVM和运行Java基础的类库。
<!-- .element: style="font-size: 24px;"--> 

通过它，Java的开发者才得以将自己开发的程序发布到用户手中，让用户使用。
<!-- .element: style="font-size: 24px;"--> 

--

### JDK (Java SE Development Kit)、JVM和JRE

![](https://beginnersbook.com/wp-content/uploads/2013/05/jdk.jpg)

JDK是Java的开发工具包。

JDK中包含JRE和一堆Java工具（javac/java/jdb等）和Java基础的类库。
<!-- .element: style="font-size: 24px;"--> 

--

### Java和JVM

![](https://beginnersbook.com/wp-content/uploads/2013/05/JVM.jpg)

所有的Java程序会首先被编译为.class的类文件，这种类型的文件可以在虚拟机上执行。
<!-- .element: style="font-size: 24px;"--> 

--

### JVM架构

![](https://beginnersbook.com/wp-content/uploads/2013/05/jvm_architecture.jpg)

Note:
Class Loader: 负责读取.class文件，并讲字节码保存到方法区。
Method Area: 所有的类都共享这一个方法区，它保存每个.class文件的类信息
Heap: 堆是JVM内存的一部分，对象所占用的内存分配在里面，JVM会给每个.class文件创建相应的类对象。
Stack: 栈也是JVM内存的一部分，但与Heap不同的是，它用于存储临时变量。
PC Registers: 用来跟踪已经执行的指令和将要执行的指令。由于指令是由线程执行的，所以每个线程都有一个单独的PC寄存器。
Native Method Stack: 本地方法可以访问虚拟机的运行时数据区域。
Native Method Interface: 使Java代码能够被本地应用程序调用。
Garbage Collection: 类实例由Java代码显式创建，使用后由垃圾收集自动销毁，用于内存管理。

---

## HotSpot虚拟机

![](https://img-blog.csdnimg.cn/20190216114129109.png)
<!-- .element: style="height: 550px;"--> 

---

## Class Loader Subsystem

类加载子系统

![](https://pic1.zhimg.com/80/v2-e29e282af3378073a72d0b1abb422dac_720w.jpg)

--

### Class Loader

类加载器

将.class文件字节码内容加载到内存中，并将这些内容转换成方法区中的运行时数据结构。

类加载器只负责加载.class文件的加载，至于它是否可以运行，则由执行引擎决定。
<!-- .element: style="font-size: 24px;"--> 

--

### 类加载器类型

- Bootstrap Class Loader 引导类加载器
<!-- .element: style="font-size: 36px;"-->  
  <p>最顶层的加载类，由C++实现，负责加载 %JAVA_HOME%/lib目录下的jar包和类或者或被 -Xbootclasspath参数指定的路径中的所有类。
<!-- .element: style="font-size: 24px;"--> 
- Extension Class Loader 扩展类加载器
<!-- .element: style="font-size: 36px;"--> 
  <p>主要负责加载目录 %JRE_HOME%/lib/ext 目录下的jar包和类，或被 java.ext.dirs 系统变量所指定的路径下的jar包。
<!-- .element: style="font-size: 24px;"--> 
- Application Class Loader 应用程序类加载器
<!-- .element: style="font-size: 36px;"--> 
  <p>面向我们用户的加载器，负责加载当前应用classpath下的所有jar包和类。
<!-- .element: style="font-size: 24px;"--> 

--

### 类加载器机制

- 全盘负责
<!-- .element: style="font-size: 36px;"-->  
  <p>当前线程的类加载器负责加载某个Class时，该Class所依赖的和引用的其他Class也将由该类加载器负责载入，除非显示使用CLassLoader.loadClass()指定类加载器来载入。
<!-- .element: style="font-size: 24px;"--> 
- 双亲委派模型
<!-- .element: style="font-size: 36px;"--> 
  <p>先让父类加载器试图加载该类，只有在父类加载器无法加载该类时才尝试从自己的类路径中加载该类。
<!-- .element: style="font-size: 24px;"--> 

--

#### 双亲委派模型

![](https://camo.githubusercontent.com/4311721b0968c1b9fd63bdc0acf11d7358a52ff6/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392d362f636c6173736c6f616465725f5750532545352539422542452545372538392538372e706e67)
<!-- .element: style="height: 550px;"--> 

---

### 类的加载过程

![](https://camo.githubusercontent.com/68465e752e28fd5e7c6a6d442c19f05305c8f043/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392d31312f2545372542312542422545352538412541302545382542442542442545382542462538372545372541382538422d2545352541452538432545352539362538342e706e67)

JVM将javac编译好的.class字节码文件加载到内存中，并对该数据进行验证、解析和初始化、形成JVM可以直接使用的JAVA类，最终回收(卸载)的过程。
<!-- .element: style="font-size: 28px;"--> 

--

### 字节码（.class）文件来源

- 从本地系统中直接加载
<!-- .element: style="font-size: 32px;"--> 
- 通过网络下载.class文件
<!-- .element: style="font-size: 32px;"--> 
- 从zip，jar等归档文件中加载.class文件
<!-- .element: style="font-size: 32px;"--> 
- 从专有数据库中提取.class文件
<!-- .element: style="font-size: 32px;"--> 
- 将Java源文件动态编译为.class文件
<!-- .element: style="font-size: 32px;"--> 

--

### 1. 加载

1. 通过全类名获取定义此类的二进制字节流
<!-- .element: style="font-size: 32px;"--> 
2. 将字节流所代表的静态存储结构转换为方法区的运行时数据结构
<!-- .element: style="font-size: 32px;"--> 
3. 在Java堆中生成一个代表这个类的java.lang.Class对象，作为对方法区中这些数据的访问入口
<!-- .element: style="font-size: 32px;"--> 

Note:
一个非数组类的加载阶段（加载阶段获取类的二进制字节流的动作）是可控性最强的阶段，这一步我们可以去完成还可以自定义类加载器去控制字节流的获取方式（重写一个类加载器的 loadClass() 方法）。数组类型不通过类加载器创建，它由 Java 虚拟机直接创建。
加载阶段和连接阶段的部分内容是交叉进行的，加载阶段尚未结束，连接阶段可能就已经开始了。

--

### 2. 链接

将Java类的二进制代码合并到JVM的运行状态中的过程。
<!-- .element: style="font-size: 36px;"--> 

1. 验证
<!-- .element: style="font-size: 32px;"--> 
   <p>验证是为了确保Class文件的字节流中包含的信息符合当前虚拟机的要求，并且不会危害虚拟机自身的安全。
   <!-- .element: style="font-size: 26px;"--> 
2. 准备
<!-- .element: style="font-size: 32px;"--> 
   <p>该阶段是在方法区中为类变量（static变量）分配内存并设置类变量初始值。例如：public static int flag = 1，在该阶段的值为0，初始化阶段才会赋值为1。
   <!-- .element: style="font-size: 26px;"--> 
3. 解析
<!-- .element: style="font-size: 32px;"--> 
   <p>虚拟机将常量池中的符号引用替换为直接引用的过程，得到类或者字段、方法在内存中的指针或者偏移量，便于后续调用。
   <!-- .element: style="font-size: 26px;"--> 

Note:
验证：文件格式验证、元数据验证、字节码验证、符号引用验证
解析：主要针对类或接口、字段、类方法、接口方法、方法类型、方法句柄和调用限定符 7类符号引用进行

--

### 3. 初始化

初始化是类加载的最后一步。静态变量会被赋予初值，静态方法区会被执行。
<!-- .element: style="font-size: 36px;"--> 

- 初始化阶段就是执行类构造器&lt;clinit>()的过程，类构造器&lt;clinit>()是由编译器自动收集类中的所有类变量的赋值动作和静态语句块中的语句合并产生的
   <!-- .element: style="font-size: 26px;"--> 
- 当初始化一个类的时候，如果发现其父类还没有进行过初始化，则需要先初始化其父类
   <!-- .element: style="font-size: 26px;"--> 
- 虚拟机会保证一个类的&lt;clinit>()方法在多线程环境中被正确加锁和同步
   <!-- .element: style="font-size: 26px;"--> 
- 当访问一个Java类的静态域时，只有正真申明这个域的类才会被初始化
   <!-- .element: style="font-size: 26px;"--> 

---

### Runtime Data Areas

运行时数据区

---

### Execution Engine 

执行引擎

---

## Android虚拟机

--

![](https://i.guancha.cn/news/2019/08/07/20190807074536162.jpg)
<!-- .element: style="height: 550px;"--> 

--

### Dalvik

--

### ART

---

## 方舟编译器


---

## 参考资料

 - [The Java® Virtual Machine Specification - Java SE 8 Edition](https://docs.oracle.com/javase/specs/jvms/se8/html/index.html)


