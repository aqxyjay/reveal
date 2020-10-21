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

### JVM和JRE
Java Runtime Environment

![](https://beginnersbook.com/wp-content/uploads/2013/05/jre.jpg)

JRE是运行基于Java语言编写的程序所不可缺少的运行环境，包括JVM和运行Java基础的类库。
<!-- .element: style="font-size: 24px;"--> 

通过它，Java的开发者才得以将自己开发的程序发布到用户手中，让用户使用。
<!-- .element: style="font-size: 24px;"--> 

--

### JDK、JVM和JRE
Java SE Development Kit

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

## 类加载子系统

Class Loader Subsystem

![](https://pic1.zhimg.com/80/v2-e29e282af3378073a72d0b1abb422dac_720w.jpg)

--

### 类加载器

Class Loader

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

### 运行时数据区

Runtime Data Areas

![](https://pic4.zhimg.com/80/v2-205a2605346856d95aec826ed9263c03_720w.jpg)

--

### 1.7以前的版本

![](https://github.com/Snailclimb/JavaGuide/raw/master/docs/java/jvm/pictures/java%E5%86%85%E5%AD%98%E5%8C%BA%E5%9F%9F/JVM%E8%BF%90%E8%A1%8C%E6%97%B6%E6%95%B0%E6%8D%AE%E5%8C%BA%E5%9F%9F.png)
<!-- .element: style="height: 550px;"--> 

--

### 1.8以后的版本

![](https://github.com/Snailclimb/JavaGuide/raw/master/docs/java/jvm/pictures/java%E5%86%85%E5%AD%98%E5%8C%BA%E5%9F%9F/2019-3Java%E8%BF%90%E8%A1%8C%E6%97%B6%E6%95%B0%E6%8D%AE%E5%8C%BA%E5%9F%9FJDK1.8.png)
<!-- .element: style="height: 550px;"--> 

--

### 数据与持有线程

#### 线程共享的
方法区  
堆  
部分直接内存（NIO）
<br>
<br>
#### 线程私有的
虚拟机栈  
本地方法栈  
程序计数器  

---

### 方法区

Method Area

用于存储已被虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。
<!-- .element: style="font-size: 36px;"--> 

- 在HotSpot虚拟机上开发、部署程序我们把方法区称为“永久代”（Permanent Generation）
<!-- .element: style="font-size: 32px;"--> 
- 其他虚拟机（如 BEA JRockit、IBM J9 等）来说是不存在永久代的概念的
<!-- .element: style="font-size: 32px;"--> 
- HotSpot虚拟机在JDK1.8中已经没有方法区的概念了，他使用元空间代替该区域
<!-- .element: style="font-size: 32px;"--> 

--

### 常用参数

JDK 1.8 之前永久代还没被彻底移除的时候通常通过下面这些参数来调节方法区大小
<!-- .element: style="font-size: 32px;"--> 
```
-XX:PermSize=N //方法区 (永久代) 初始大小
-XX:MaxPermSize=N //方法区 (永久代) 最大大小，超过这个值将会抛出 OutOfMemoryError 异常:java.lang.OutOfMemoryError: PermGen
```

JDK 1.8 的时候，方法区被元空间取代
<!-- .element: style="font-size: 32px;"--> 
```
-XX:MetaspaceSize=N //设置 Metaspace 的初始（和最小大小）
-XX:MaxMetaspaceSize=N //设置 Metaspace 的最大大小
```

与永久代很大的不同就是，如果不指定大小的话，随着更多类的创建，虚拟机会耗尽所有可用的系统内存。
<!-- .element: style="font-size: 24px;"--> 

--

### Why

为什么要将永久代 (PermGen) 替换为元空间 (MetaSpace) 呢？

Note:
1. 整个永久代有一个 JVM 本身设置固定大小上限，无法进行调整，而元空间使用的是直接内存，受本机可用内存的限制，虽然元空间仍旧可能溢出，但是比原来出现的几率会更小。
当你元空间溢出时会得到如下错误： java.lang.OutOfMemoryError: MetaSpace
你可以使用 -XX：MaxMetaspaceSize 标志设置最大元空间大小，默认值为 unlimited，这意味着它只受系统内存的限制。-XX：MetaspaceSize 调整标志定义元空间的初始大小如果未指定此标志，则 Metaspace 将根据运行时的应用程序需求动态地重新调整大小。
2. 元空间里面存放的是类的元数据，这样加载多少类的元数据就不由 MaxPermSize 控制了, 而由系统的实际可用空间来控制，这样能加载的类就更多了。
3. 在 JDK8，合并 HotSpot 和 JRockit 的代码时, JRockit 从来没有一个叫永久代的东西, 合并之后就没有必要额外的设置这么一个永久代的地方了。

---

### 堆区

Heap Area

堆的唯一目的就是存放对象的实例，*几乎所有*对象实例都在堆中分配内存。

堆是JVM所管理的内存中最大的一块，Java 堆是所有线程共享的一块内存区域，在虚拟机启动时创建。
<!-- .element: class="fragment visible"--> 

堆是垃圾收集器管理的主要区域，因此也被称作GC 堆（Garbage Collected Heap）
<!-- .element: class="fragment visible"--> 

--

### 1.7以前堆的细分

在 JDK 1.7 版本及以前，堆被分为下面三部分：

- 新生代内存(Young Generation)：Eden 区和Survivor 区
- 老生代(Old Generation)
- 永生代(Permanent Generation)

![](https://github.com/Snailclimb/JavaGuide/raw/master/docs/java/jvm/pictures/java%E5%86%85%E5%AD%98%E5%8C%BA%E5%9F%9F/JVM%E5%A0%86%E5%86%85%E5%AD%98%E7%BB%93%E6%9E%84-JDK7.png)

--

### 1.8以后堆的细分

![](https://github.com/Snailclimb/JavaGuide/raw/master/docs/java/jvm/pictures/java%E5%86%85%E5%AD%98%E5%8C%BA%E5%9F%9F/JVM%E5%A0%86%E5%86%85%E5%AD%98%E7%BB%93%E6%9E%84-jdk8.png)

JDK 8 版本之后方法区（HotSpot 的永久代）被彻底移除了，取而代之是元空间，元空间使用的是直接内存。

--

### 任期的计算

1. 大部分情况，对象都会首先在 Eden 区域分配
2. 在一次新生代垃圾回收后，如果对象还存活，则会进入下一个Survivor区，任期+1
3. 当对象的任期大小超过了Survivor区的一半或达到阈值时，就会被晋升到老年代中
4. 对象晋升到老年代的任期阈值，可以通过参数 -XX:MaxTenuringThreshold 来设置

Note:
Hotspot遍历所有对象时，按照任期从小到大对其所占用的大小进行累积，当累积的某个任期大小超过了Survivor区的一半时，取这个任期和MaxTenuringThreshold中更小的一个值，作为新的晋升任期阈值

--

### 堆内存溢出

- OutOfMemoryError: GC Overhead Limit Exceeded  
  当JVM花太多时间执行垃圾回收并且只能回收很少的堆空间时，就会发生此错误
  <!-- .element: style="font-size: 32px;"--> 
- OutOfMemoryError: Java heap space  
  假如在创建新的对象时, 堆内存中的空间不足以存放新创建的对象，就会发生此错误
  <!-- .element: style="font-size: 32px;"--> 

---

### 虚拟机栈

VM Stack Area

虚拟机栈是描述 Java 方法运行过程的内存模型。
<!-- .element: class="fragment visible"--> 

它的生命期与线程的生命期保持一致。
<!-- .element: class="fragment visible"--> 

对于每个方法调用，将在栈存储器中产生称为栈帧。
<!-- .element: class="fragment visible"--> 


--

### 栈帧的构成

每个栈帧中都拥有：局部变量表、操作数栈、动态链接、方法出口信息。

![](https://github.com/doocs/jvm/raw/master/docs/images/jvm-stack.jpg)
<!-- .element: style="height: 400px;"--> 

局部变量表随着栈帧的创建而创建，它的大小在编译时确定，不会发生改变。
<!-- .element: style="font-size: 32px;"--> 

Note:
局部变量表主要存放了编译期可知的各种数据类型（boolean、byte、char、short、int、float、long、double）、对象引用（reference 类型，它不同于对象本身，可能是一个指向对象起始地址的引用指针，也可能是指向一个代表对象的句柄或其他与此对象相关的位置）。
操作数堆栈（Operand stack）：如果需要执行任何中间操作，操作数堆栈将充当运行时工作空间来执行操作
帧数据（Frame Data）：对应于方法的所有符号存储在此处。在任何异常的情况下，捕获的区块信息将被保持在帧数据中；

--

### 栈溢出和内存溢出

Java 虚拟机栈会出现两种异常：StackOverFlowError 和 OutOfMemoryError。

- StackOverFlowError  
  若 Java 虚拟机栈的大小不允许动态扩展，那么当线程请求栈的深度超过当前 Java 虚拟机栈的最大深度时，抛出 StackOverFlowError 异常。
  <!-- .element: style="font-size: 28px;"--> 
- OutOfMemoryError  
  若允许动态扩展，那么当线程请求栈时内存用完了，无法再动态扩展时，抛出 OutOfMemoryError 异常。
  <!-- .element: style="font-size: 28px;"--> 

可以通过如下参数配置栈的大小：
```
-Xss 2m // 一般虚拟机会有最大值和最小值的限制
```

---

### 本地方法栈

Native Method Stack

为 JVM 运行 Native 方法准备的空间。
<!-- .element: class="fragment visible"--> 

与 Java 虚拟机栈实现的功能类似。
<!-- .element: class="fragment visible"--> 

是描述本地方法运行过程的内存模型。
<!-- .element: class="fragment visible"--> 

HotSpot虚拟机把本地方法栈和虚拟机栈合二为一。
<!-- .element: class="fragment visible"--> 

---

### 程序计数器

Program Counter Register

用于保存当前执行指令的地址。
<!-- .element: class="fragment visible"--> 

主要有两个作用：
<!-- .element: class="fragment visible"--> 
- 执行引擎中的字节码解释器通过改变程序计数器来依次读取指令，从而实现代码的流程控制，如：顺序执行、选择、循环、异常处理
<!-- .element: style="font-size: 28px;" class="fragment visible"-->
- 在多线程的情况下，程序计数器用于记录当前线程执行的位置，从而当线程被切换回来的时候能够知道该线程上次运行到哪儿了
<!-- .element: style="font-size: 28px;" class="fragment visible"--> 
---

### 执行引擎

Execution Engine 

负责执行运行时数据区的字节码。

#### 包含三部分
解释器(Interpreter)  
JIT编译器(Just In Time Compiler)  
垃圾收集器(Garbage Collector)  

--

### 解释器

负责把.class字节码翻译为机器码。

缺点：当一个方法被调用多次时，每次都需要进行解释

--

### JIT编译器

![](https://www.ibm.com/developerworks/cn/java/j-lo-just-in-time/img001.png)
<!-- .element: style="height: 550px;"--> 

--

### 垃圾收集器

Java 的自动内存管理主要是针对对象内存的回收和分配。

最核心的功能是 **堆** 内存中对象的分配与回收。

[JVM 垃圾回收 - JavaGuide - GitHub](https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/jvm/JVM%E5%9E%83%E5%9C%BE%E5%9B%9E%E6%94%B6.md#1--%E6%8F%AD%E5%BC%80-jvm-%E5%86%85%E5%AD%98%E5%88%86%E9%85%8D%E4%B8%8E%E5%9B%9E%E6%94%B6%E7%9A%84%E7%A5%9E%E7%A7%98%E9%9D%A2%E7%BA%B1)
<!-- .element: class="fragment visible"--> 

---

## Android虚拟机

--

### 发展时间线

![](https://i.guancha.cn/news/2019/08/07/20190807074536162.jpg)
<!-- .element: style="height: 550px;"--> 

---

### Dalvik与JVM的区别

--

### 基于的架构不同

JVM基于栈架构

Dalvik基于寄存器架构

Note:
基于栈的架构具有更好的可移植性，因为其实现不依赖于物理寄存器
基于栈的架构通常指令更短，因为其操作不需要指定操作数和结果的地址
基于寄存器的架构通常运行速度更快，因为有寄存器的支撑
基于寄存器的架构通常需要较少的指令来完成同样的运算，因为不需要进行压栈和出栈

--

### 执行字节码不同

JVM通过解码class文件来运行程序

Dalvik通过解码dex文件来运行程序

![](https://qiangbo-workspace.oss-cn-shanghai.aliyuncs.com/AndroidNewFeatureBook/Chapter3/jar_vs_dex.png)
<!-- .element: style="height: 400px" class="fragment visible"--> 

Note:
jar文件以class为区域进行划分，在连续的class区域中会包含每个class中的常量，方法，字段等等。而dex文件按照类型（例如：常量，字段，方法）划分，将同一类型的元素集中到一起进行存放。这样可以更大程度上避免重复，减少文件大小。

--

### Dalvik允许在有限的内存中同时运行多个进程

Dalvik经过优化，允许在有限的内存中同时运行多个进程。

在Android中每一个应用都运行在一个Dalvik实例中。

每一个Dalvik实例都运行在一个独立的进程空间，独立的进程可以防止虚拟机崩溃时所有程序都被关闭。

--

### Dlavik由Zygote创建并初始化

Zygote是一个Dlavik进程，同时也用来创建和初始化其他Dlavik进程。

每当系统需要一个应用程序进程的时候，Zygote就会fork自身，快速地创建和初始化一个Dlavik实例，用于程序运行。

对于一些只读的系统库，所有的Dlavik实例都会和Zygote共享一块内存区域，节省内存开销。

--

### Dlavik有共享机制

Dlavik拥有预加载-共享机制，不同应用之间运行时可以共享相同的类，拥有更高的效率。

而JVM机制不存在这种共享机制，不同的程序，打包以后程序都是彼此独立的，即便是他们使用了相同的类，运行时也都是单独加载和运行的。

--

### 早期没有JIT编译器

JVM使用了JIT（Just In Time Compiler），而Dlavik早期没有使用JIT编译器。

Android 2.2之后开始为DVM使用了JIT编译器。

---

### ART与Dalvik的区别

--

### AOT和JIT

在ART中，系统安装应用程序时会进行一次AOT（Ahead of Time Compilation），将字节码预编译成机器码并存储在本地。

缺点：安装慢、占用空间大。

Android 7.0版本中的ART加入了JIT即时编译器。

--

### ARM和ARM64

Dalvik是为32位CPU设计的。

ART是支持64位并且兼容32位CPU.

--

### 垃圾回收

ART对垃圾回收机制进行了改进。

更频繁的执行并行垃圾收集。

将GC暂停由2次减少为1次。

---

## 方舟编译器

方舟编译器是为支持多种编程语言、多种芯片平台的联合编译、运行而设计的统一编程平台，包含编译器、工具链、运行时等关键部件。
<!-- .element: style="font-size: 28px;"-->

生来就是为了干掉虚拟机。
<!-- .element: class="fragment visible"--> 

--

### 预编译语言/编译语言

![](https://i.guancha.cn/news/2019/08/07/20190807074535622.jpg)
<!-- .element: style="height: 550px;"-->

--

### Android四大命门

1. Java的虚拟机
2. Java的“原罪” - 额外的JNI开销
3. 代码优化空间有限
4. Java现有内存回收机制易造成间歇性卡顿

--

### 干掉虚拟机

- 遍历Java的动态语义，进行了大规模的数据建模
- 在运行时高效获得动态信息

把预编译语言，编译成机器码。

--

### 干掉JNI

![](https://i.guancha.cn/news/2019/08/07/20190807074539525.jpg)

--

### 编译优化

![](https://i.guancha.cn/news/2019/08/07/20190807074539658.jpg)

--

### 实时回收

![](https://i.guancha.cn/news/2019/08/07/20190807074539971.jpg)


---

## 参考资料

- [十分钟带你了解JVM的结构体系 - 青糜 - 知乎专栏](https://zhuanlan.zhihu.com/p/102702428)
<!-- .element: style="font-size: 28px;"-->
- [JVM 架构解析 - 文西 - 知乎专栏](https://zhuanlan.zhihu.com/p/38858242)
<!-- .element: style="font-size: 28px;"-->
- [Java 内存区域详解 - JavaGuide - GitHub](https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/jvm/Java%E5%86%85%E5%AD%98%E5%8C%BA%E5%9F%9F.md)
<!-- .element: style="font-size: 28px;"-->
- [你了解JVM中的 JIT 即时编译及优化技术吗？ - 云大数据社区 - 简书](https://www.jianshu.com/p/fbced5b34eff)
<!-- .element: style="font-size: 28px;"-->
- [The Java® Virtual Machine Specification - Java SE 8 Edition](https://docs.oracle.com/javase/specs/jvms/se8/html/index.html)
<!-- .element: style="font-size: 28px;"-->
- [Java虚拟机与垃圾回收算法 - paul.pub](https://paul.pub/android-java-vm/)
<!-- .element: style="font-size: 28px;"-->
- [Android上的Dalvik虚拟机 - paul.pub](https://paul.pub/android-dalvik-vm/)
<!-- .element: style="font-size: 28px;"-->
- [Android上的ART虚拟机 - paul.pub](https://paul.pub/android-art-vm/)
<!-- .element: style="font-size: 28px;"-->
- [方舟编译器/OpenArkCompiler - Gitee](https://gitee.com/openarkcompiler/OpenArkCompiler)
<!-- .element: style="font-size: 28px;"-->
- [首次全面深度解密华为方舟编译器 - 菊厂搞机MO](https://www.openarkcompiler.cn/news/detail/news5)
<!-- .element: style="font-size: 28px;"-->