# 好代码

Good Code

---

## 烂代码

--

### 样例

```c
void _(int __, int ___, int ____, int _____)
{
    ((___ / __) <= _____) ? _(__,___+_____,____,_____) : !(___ % __) ? _(__,___+_____,___ % __, _____) :
    ((___ % __)==(___ / __) && !____) ? (printf("%d\n",(___ / __)),
    _(__,___+_____,____,_____)) : ((___ % __) > _____ && (___ % __) < (___ / __)) ?
    _(__,___+_____,____ + !((___ / __) % (___ % __)),_____) : (___ < __ * __) ?
    _(__,___+_____,____,_____) : 0;
}

int main() {
    _(100,0,0,1);
}
```

---

## 如何写出烂的代码

> 什么叫“创造力”，创造力就是：就算是要干一件烂事都能干得那么漂亮那么有创意的能力。

---

### 程序命名

--

#### 要使用容易输入的名字

```c
int fred;
int asdf;
bool aaa;
```

--

#### 要使用单个字母的名字

```c
int a;
bool b;
int x, y ,z;
int a1, a2, a3;
```

--

#### 有创意地拼写错误

```java
class Portal {
    void openPartal();
    void closePortle();
}

```

--

#### 要用近义词

比如：用Scope替代Range。

```java
class Scope {
    /**
     * Obtains the lower bound of the current range.
     */
    T getLower​();
    /**
     * Obtains the upper bound of the current range.
     */
    T getUpper();
}
```

[Scope vs Range - What's the difference?](https://wikidiff.com/scope/range#:~:text=As%20nouns%20the%20difference%20between%20scope%20and%20range,travel%20%28over%29%20%28an%20area%2C%20etc%29%3B%20to%20roam%2C%20wander.)

--

#### 要用中式英语

```java
class ServiceTest {
    void testServiceNoDie();
}
```

--

#### 把抽象应用到命名的方方面面

```c
struct Data {};
struct Data *GetData();
```

--

#### 一定要用缩写！

```java
class WTFService {}

// Wait to Friday Service
```

--

#### 拼音缩写效果更好

```java
class BTProfile {
    int maxCountTJJTDS = 10000;
}
```

--

#### 使用随机的大小写

```c
int gEtnuMbER();
```

--

#### 记得重复使用变量名

```c
int main(void){
  int x=0;

  x = atoi(char_var);

  for (x=0; x<12; x++){
   //...
  }

  x = socket(...)
  if(x<0){
    //...
  }

  for(x=0;x<100;x++{
    //...
  }

  return 0;
}
```

--

#### 多使用下划线

```c
void _(int __, int ___, int ____, int _____)
{
    ((___ / __) <= _____) ? _(__,___+_____,____,_____) : !(___ % __) ? _(__,___+_____,___ % __, _____) :
    ((___ % __)==(___ / __) && !____) ? (printf("%d\n",(___ / __)),
    _(__,___+_____,____,_____)) : ((___ % __) > _____ && (___ % __) < (___ / __)) ?
    _(__,___+_____,____ + !((___ / __) % (___ % __)),_____) : (___ < __ * __) ?
    _(__,___+_____,____,_____) : 0;
}

int main() {
    _(100,0,0,1);
}
```

--

#### 英语不会时，拼音来凑

```javascript
class Car {
    Engine engine;
    BianSuXiang bsx;
    GuLus gls;
}
```

--

#### 使用符号名称来命名

```java
long comma = 1l;
float slash = 0.1f
int equal = comma / slash;
```

---

### 伪装欺诈

--

#### 把注释和代码交织在一起

```java
for(j=0; j<array_len; j+=8)
{
    total += array[j+0 ];
    total += array[j+1 ];
    total += array[j+2 ]; /* Main body of
    total += array[j+3]; * loop is unrolled
    total += array[j+4]; * for greater speed.
    total += array[j+5]; */
    total += array[j+6 ];
    total += array[j+7 ];
}
```

--

#### 把宏定义藏起来

```c
#define a=b a=0-b
```

--

#### 要善用typedef和struct

```c
typedef struct {
  char* pTr;
  size_t lEn;
} snafu;

struct snafu {
  unsigned cNt
  char* pTr;
  size_t lEn;
} A;
```

--

#### 写一些“很忙”的代码

```c
#define fastcopy(x,y,z) /*xyz*/
...
fastcopy(array1, array2, size); /* does nothing */
```

--

#### 给宏定义换个行

```c
#define local_var xy_z // not bad

#define local_var xy\
_z // bad enough
```

--

#### 多定义几层宏

```c
#define xxx global_var // in file std.h
#define xy_z xxx // in file ..\other\substd.h
#define local_var xy_z // in file ..\codestd\inst.h
```

--

#### 预编译和宏定义

```c++
#ifndef DONE
#ifdef TWICE
// put stuff here to declare 3rd time around
void g(char* str);
#define DONE
#else // TWICE
#ifdef ONCE
// put stuff here to declare 2nd time around
void g(void* str);
#define TWICE
#else // ONCE
// put stuff here to declare 1st time around
void g(std::string str);
#define ONCE
#endif // ONCE
#endif // TWICE
#endif // DONE
```

Note:
在头文件中使用预编译来查看这个头文件被include了几次，而被include不同的次数时，其中的函数定义完全不一样。

--

#### 取一个欺诈的名字

```java
class Parser {
    int ilI1;
    int oO08;

    int parselnt();
}
```
```java
class Swimmer {
    Swimmer swimner;

    void swin();
};
```
```c
int x_yz, xy_z, xY_z, xy__z;
```

--

#### 在不同的地方取不同的名字

```
companyName = "mars"
```

```java
String corperationName = getName("companyName");
```

```json
{
    "mars":"ByteDance"
}
```

```javascript
logo.innerText = json.mars;
```

--

#### 重载函数

```java

public setData(Data data) {
    this.data = data;
}

public setData(Object obj) {
    this.obj = obj;
}

```

--

#### 操作符重载

假设重载了一个`!`操作符，让其返回一个整数。

```c++
int operator!()
{
    return 1;
}

// !!val ?
```

---

### 换一种方式

> 条条大路通罗马

怎么用Java反转一个整数的符号，比如把+12转成-12？
<!-- .element: class="fragment visible"--> 

--

#### 第1条路

```java
public static int invert(int n) {
    return -n;
}
```

--

#### 第2条路

```java
public static int invert(int n) {
    return (0xffffffff ^ n) + 1;
}
```

--

#### 第3条路

```java
public static int invert(int n) {
    return ~n + 1;
}
```

--

#### 第4条路

```java
public static int invert(int n) {
    return ~--n
}
```

--

#### 第5条路

```java
public static int invert(int n) {
    return n - (n + n);
}
```

--

#### 第6条路

```java
public static int invert(int n) {
    switch (n)
        case 1: return -1;
        case 2: return -2;
        case 3: return -3;
        // ... etc, you get the proper pattern
}
```

--

#### 第7条路

```java
public static int invert(int n) {
    int x = n;
    boolean pos = x > 0;
    for(int i = 0; i < 2 * Math.abs(x); i++){
        if(pos){
            n--;
        }
        else{
            n++;
        }
    }
    return n;
}
```

--

#### 第8条路

```java
public static int invert(int n) {
    n ^= 0xffffffff;
    int m;
    for (m = 1; m != 0 && ((n&m) != 0); m <<= 1);
    n |= m;
    if (m == 0) n= m;
    else for (m >>= 1; m != 0; n ^= m, m >>=1);
    return n;
}
```

--

#### 第9条路

```java
public static int invert(int n) {
    String nStr = String.valueOf(n);
    if (nStr.startsWith("-")) {
        nStr = nStr.replace("-", "");
    } else {
        nStr = "-" + nStr;
    }
    return Integer.parseInt(nStr);
}
```

--

#### 第10条路

```java
public interface Negatable<T extends Number> {
  T value();
  T negate();
}

public abstract class NegatableInteger implements Negatable<Integer> {
  private final int value;
 
  protected NegatableInteger(int value) {
    this.value = value;
  }
 
  public static NegatableInteger createNegatableInteger(int value) {
    if (value > 0) {
      return new NegatablePositiveInteger(value);
    }
    else if (value == Integer.MIN_VALUE) {
      throw new IllegalArgumentException("cannot negate " + value);
    }
    else if (value < 0) {
      return new NegatableNegativeInteger(value);
    }
    else {
      return new NegatableZeroInteger(value);
    }
  }
 
  public Integer value() {
    return value;
  }
 
  public Integer negate() {
    String negatedString = negateValueAsString ();
    Integer negatedInteger = Integer.parseInt(negatedString);
    return negatedInteger;
  }
 
  protected abstract String negateValueAsString ();
}

public class NegatablePositiveInteger extends NegatableInteger {
  public NegatablePositiveInteger(int value) {
    super(value);
  }
 
  protected String negateValueAsString () {
    String valueAsString = String.valueOf (value());
    return "-" + valueAsString;
  }
}

public class NegatableNegativeInteger extends NegatableInteger {
  public NegatableNegativeInteger (int value) {
    super(value);
  }
 
  protected String negateValueAsString () {
    String valueAsString = String.valueOf (value());
    return valueAsString.substring(1);
  }
}

public class NegatableZeroInteger extends NegatableInteger {
  public NegatableZeroInteger (int value) {
    super(value);
  }
 
  protected String negateValueAsString () {
    return String.valueOf (value());
  }
}

public static int invert(int n) {
    return NegatableInteger.createNegatableInteger(n).negate();
}
```

---

### 文档和注释

--

#### 在注释中“说谎”

```java
/**
 * Set the data as the data.
 *
 * @param obj The object of an object.
 */
public void setData(Data data);
```

不用真的去撒谎，只需在改代码的时候不要更新注释就可以了。
<!-- .element: class="fragment visible"--> 

--

#### 注释明显的逻辑

```java
public void addadd(n) {
    // add 1 to n
    return n++;
}
```

--

#### 不要注释度量单位

```java
int timeout = 3000;
int length = 32;
int maxFilesize = 1024;
```

Note:
比如时间用的是秒还是毫秒，尺寸用的是像素还是英寸，大小是MB还是KB。等等。另外，在你的代码里，你可以混用不同的度衡单位，但也不要注释。

--

#### 不要注释代码里的陷阱

> 1. 不要把陷阱改掉
> 2. 不要加注释说明陷阱
 
这样别人就可以和你一样掉下去了。
<!-- .element: class="fragment visible"--> 

--

#### 在文档和注释里发泄不满

```php
//When I wrote this, only God and I understood what I was doing
//Now, God only knows
```

---

### 程序设计

--

#### 善用Java的强转

```java
Map<Sting, Object> objs = ...;
Data date = (Data) objs.get("data");
```

--

#### 善用Java的实例声明方式

```java
Bubblegum b = new Bubblegom();
```

--

#### 不要验证入参

```java
public void invokeIt(Call call) {
    call.invoke();
}
```

这样做可以向大家展示你是多么的信任公司的设备和其它程序员。
<!-- .element: class="fragment visible"--> 

--

#### 不要抽取方法

```java
public void complex() {
    int a;
    // do task a
    for ...
    // do task b
    for ...
    // do task c
    ...
}
```

调用者需要知道被调用的所有的细节。
<!-- .element: class="fragment visible"--> 

--

#### 多用Ctrl-C Ctrl-V

为了开发效率，你要学会使用copy + paste。

你几乎都不用理解别人的代码，你就可以高效地编程了。
<!-- .element: class="fragment visible"--> 

--

#### 写一个超大的Listener

```java
class ButtonListener {
    void onClick(Event evt) {
        if (evt.key === 'A') ...;
        else if (evt.key === 'B') ...;
        ...
        ...
    }
}
```

--

#### 混用属性访问方式

```java
public class Profile {
    public String name;
    public int age;

    public int getAge() {
        return this.age;
    }
    
    public void setAge(int age) {
        this.aget = age;
    }
}
```

这样还有一个“好处”，你以后就很难限制其被人使用，而且这样可以和别的代码造成更多的耦合度，可以让你的代码存活得更久。
<!-- .element: class="fragment visible"--> 

--

#### xyz?yxz?zxy?

```javascript
function draw3DPoint(y, x, z);
```

过几个版本，再改成z,y,z，有奇效。
<!-- .element: class="fragment visible"--> 

--

#### 给你的代码加上final

```java
public final class FTP {
    public final int connect(String ip, int port);
    public final int upload(String fileName);
    public final int download(String fileName);
}
```

这样，当你做完这个项目后，没有人可以通过继承来扩展你的类。java.lang.String不也是这样吗？
<!-- .element: class="fragment visible"--> 

--

#### 使用全局变量

```java
public class Data {
    public int a;
    public int b;

    public init() {
        b = 0;
    }

    public reset() {
        a = b;
    }
}
```

Note:
1）把全局变量的初始化放在不同的函数中，就算这个函数和这个变量没有任何关系，这样能够让我们的维护人员就像做侦探工作一样。2）使用全局变量可以让你的函数的参数变得少一些。

--

#### 把所有功能都放在一个类中

```java
class Car {
    void drive();
    void gearUp();
    void powerOff();
    balabala...
}
```

---

### 制造混乱

--

#### 使用XML

```xml
<rootNode>
   <numberOfAddresses>110</numberOfAddresses>
   <address_1>442 Fake St.</address_1>
   <address_2>61 Main St.</address_2>
   ...
   ...
   ...
   <address_110>3881 N 4th Ave. #5D</address_110>
</rootNode>
```

Note:
XML的强大是无人能及的。使用XML你可以把本来只要10行的代码变成100行。而且，还要逼着别人也有XML。

--

#### 使用不同的进制

```c
array = new int[]
{
   111,
   120,
   013,
   121,
};
```

--

#### 使用void*

```c
void cast(void *obj) {
    struct Data data = (struct Data *)obj;
    struct Datum datum = (struct Datum *)obj;
}
```

--

#### 使用隐式转换

```c++
class Test
{
    public:
        Test(int i); // inexplicit
};

Test t1 = 1;
Test t2(1);
```

Note:
由于强制类型转换，1先被Test构造函数构造成Test对象，然后才被赋值给t1。

--

#### 分解条件表达式

```
a>99 && a<101
```

--

#### 学会利用分号

```
if (a);else;{int d; d = c;}
```

--

#### 间接转型

```java
String dStr = new Double(d).toString();
```

--

#### 使用C的变种数组

```c
int a = myArray[i];
int b = *(myArray + i);
int c = *(i + myArray);
int d = i[myArray];
```

```c
int myfunc(int q, int p) { return p%q; }
...
myfunc(6291, 8)[myArray];
```

---

### 测试

--

#### 不要测试

> 千万不要测试任何的逻辑，从来也不检测系统调用的返回值。

--

#### 永远不做性能测试

> 如果不够快就告诉用户换一个更快的机器。

--

#### 不要写测试用例

> 不要做什么代码覆盖率测试，自动化测试。

--

#### “测试是懦夫的行为”

> 一个勇敢的程序员是根本不需要这一步的。

Note:
太多的程序太害怕他们的老板，害怕失去工作，害怕用户抱怨，甚至被起诉。这种担心害怕直接影响了生产力。如果你对你的代码有强大的信心，那还要什么测试呢？真正的程序员是不需要测试自己的代码的。

---

### 声明

> 以上内容仅用于识别烂代码，请勿应用于工程实践。

---

## 写出好代码的建议

--

### DRY: Don’t repeat yourself

它意味着，当我们在两个或多个地方的时候发现一些相似的代码的时候，我们需要把他们的共性抽象成为一个唯一的新方法，并且改变现有的地方的代码让他们以一些合适的参数调用这个新的方法。

> 作者注：测试代码也要DRY
<!-- .element: class="fragment visible"--> 

--

### 短小的方法

1. 代码会变得更容易阅读
2. 代码会变得更容易重用
3. 短方法可以减少代码间的耦合
4. 代码会变得更容易测试

> 作者注：50行也挺长的
<!-- .element: class="fragment visible"--> 

--

### 良好的命名规范

当一个类，一个函数，一个变量的名字达到了那种可以“望文生义”的境界话，我们就可以少一些文档，少一些沟通。

--

### 赋予每个类正确的职责

这里强调的不是类的单一职责，而是一种正确的职责。

如果你有一个类叫Customer，我们就不应该让这个类有sales 的方法，我们只能让这个类有和Customer有最直接关系的方法。

--

### 把代码组织起来

 - 物理层组织  
   通过目录、包名、命名空间等方式，把代码组织起来，目的是方便分类和查找。
 - 逻辑层组织  
   把不同功能的类或方法通过规范联系或组织起来，也就是模块或架构设计，重点关注模块与模块之间的接口。

--

### 创建大量的单元测试

单元测试是最接近BUG的地方，也是修改BUG成本最低的地方，同样也是决定整个软件质量好坏的成败的地方。


它可以保证你未来改变相应代码的时候，可以很简单知道这些改变是否影响了其它单元。

--

### 经常重构你的代码

软件开发是一种持续的发现的过程，从而让你的代码可以跟上最新的实际需求的变化。所以，我们要经常重构自己的代码来跟上这样的变化。

1. 有大量的单元测试来保证功能
2. 每次重构都不要大，用点点滴滴的小的重构来代替那种大型的重构。

--

### 程序注释是邪恶的

在实际过程当中，程序员们写出来的注释却是很糟糕的。表达能力是一方面，换位思考也是一方面。

注释往往都是过时的。

--

### 注重接口，而不是实现

接口相当于一种合同契约，而实际的细节相当于对这种合同契约的一种运作和实现。运作是可以很灵活的，而合同契约则需要是相对需要稳定和不变的。

程序员总是注重于实现细节，所以他们局部的代码写的非常不错，但软件整体却设计得相对较差。
<!-- .element: class="fragment visible"--> 

--

### 代码审查机制

所有人都会出错，一个人出错的概率是很大的，两个人出错的概率就会小一些，人多一些，出错的概率就会越来越小。

- 审查者的能力一定要大于或等于代码作者的能力，不然，代码审查就成了一种对新手的培训
- 需要让审查者对审查过的代码负主要责任，而不是代码的作者
- 好的代码审查应该不是当代码完成的时候，而是在代码编写的过程中

---

## 一些实用的软件设计原则

--

### Don’t Repeat Yourself (DRY)

当我们在两个或多个地方的时候发现一些相似的代码的时候，我们需要把他们的共性抽象成唯一的一个新方法。

> 作者注：把几处相似的代码抽象到一处，为的是将来少修改几个地方。
<!-- .element: class="fragment visible"--> 

--

### Keep It Simple, Stupid (KISS)

把一个事情搞复杂是一件简单的事，但要把一个复杂的事变简单，这是一件复杂的事。

> 作者注：主要还是为了少写点代码。
<!-- .element: class="fragment visible"--> 

--

### You Ain’t Gonna Need It (YAGNI)
只考虑和设计必须的功能，避免过度设计。

只实现目前需要的功能，在以后您需要更多功能时，可以再进行添加。

> 作者注：又可以少写一些代码了。
<!-- .element: class="fragment visible"--> 

--

### Law of Demeter – 迪米特法则

又称“最少知识原则”（Principle of Least Knowledge）。又称作“不要和陌生人说话”。

如果你去店里买东西，你会把钱交给店员，还是会把钱包交给店员让他自己拿？

> 作者注：方便他人也是方便自己。
<!-- .element: class="fragment visible"--> 

--

### 面向对象的S.O.L.I.D 原则

- Single Responsibility Principle (SRP) – 职责单一原则
- Open/Closed Principle (OCP) – 开闭原则
- Liskov substitution principle (LSP) – 里氏代换原则
- Interface Segregation Principle (ISP) – 接口隔离原则
- Dependency Inversion Principle (DIP) – 依赖倒置原则

> 作者注：主要目的是以后不改了。
<!-- .element: class="fragment visible"--> 

--

### 总结一下

> “懒”，才是第一生产力。
<!-- .element: class="fragment visible"--> 

---

## 链接分享

- [酷壳 - CoolShell](https://coolshell.cn/)
- [系统设计入门 - GitHub](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md)
- [对开发人员有用的定律、理论、原则和模式 - GitHub](https://github.com/nusr/hacker-laws-zh)

---

## 参考资料

- [unmaintainable code - mindprod](https://www.mindprod.com/jgloss/unmaintesting.html)
- [如何写出无法维护的代码 - coolshell](https://coolshell.cn/articles/4758.html)
- [编程真难啊 - coolshell](https://coolshell.cn/articles/1391.html)
- [如何加密/混乱C源代码 - coolshell](https://coolshell.cn/articles/933.html)
- [优质代码的十诫 - coolshell](https://coolshell.cn/articles/1007.html)
- [一些软件设计的原则 - coolshell](https://coolshell.cn/articles/1007.html)


---

## 如何重构出烂代码

--

### 开始程序

```c
void primes(int cap)
{
    int i, j, composite;
    for(i = 2; i < cap; ++i) {
        composite = 0;
        for(j = 2; j * j < i; ++j) {
            composite += !(i % j);
        }
        if(!composite){
            printf("%d\n", i);
        }
    }
}
int main()
{
    primes(100);
}
```

--

### 步骤1：把for变成while

```c
void primes(int cap)
{
    int i, j, composite, t = 0;
    while(t < cap * cap) {
        i = t / cap;
        j = t++ % cap;
        if(i <= 1);
        else if(!j)
            composite = j;
        else if(j == i && !composite)
            printf("%d\n",i);
        else if(j > 1 && j < i)
            composite += !(i % j);
    }
}
int main()
{
    primes(100);
}
```
Note:
通常来说，for循坏要以while循坏简单一些，上面的程序有二重for循环，我们不但要把其变成while循环，而且还要把二重循环的变成一重的循环，然后使用大量的if-else语句来判断。

--

### 步骤2：把循坏变成递归

```c
void primes(int cap, int t, int composite)
{
    int i,j;
    i = t / cap;
    j = t % cap;
    if(i <= 1)
        primes(cap,t+1,composite);
    else if(!j)
        primes(cap,t+1,j);
    else if(j == i && !composite)
        (printf("%d\n",i), primes(cap,t+1,composite));
    else if(j > 1 && j < i)
        primes(cap,t+1, composite + !(i % j));
    else if(t < cap * cap)
        primes(cap,t+1,composite);
}

int main()
{
    primes(100,0,0);
}
```

Note:
递归在某些时候是可以把代码变得简单，但大多数的情况下是把代码变得复杂，而且很没有效率。下面是把上面的while循环变成了递归。变成了递归后，函数的参数都变成3个了。

--

### 步骤3：弄乱代码结构/使用没有含义的变量名

```c
void primes(int m, int t, int c)
{
    int i,j;
    i = t / m;
    j = t % m;
    (i <= 1) ? primes(m,t+1,c) : (!j) ? primes(m,t+1,j) : (j == i && !c) ?
    (printf("%d\n",i), primes(m,t+1,c)) : (j > 1 && j < i) ?
    primes(m,t+1,c + !(i % j)) : (t < m * m) ? primes(m,t+1,c) : 0;
}

int main()
{
    primes(100,0,0);
}
```

Note:
关于如何弄乱代码结构，其中一个小技巧是，使用“？”表达式代替if-else语句。

--

### 步骤4：取消临时变量

```c
void primes(int m, int t, int c)
{
  ((t / m) <= 1) ? primes(m,t+1,c) : !(t % m) ? primes(m,t+1, t % m) :
  ((t % m)==(t / m) && !c) ? (printf("%d\n",(t / m)), primes(m,t+1,c)) :
  ((t % m)> 1 && (t % m) < (t / m)) ? primes(m,t+1,c + !((t / m) % (t % m))) :
  (t < m * m) ? primes(m,t+1,c) : 0;
}

int main()
{
    primes(100,0,0);
}
```

Note:
临时变量一般用来保存反复使用的一个表达式的值。使用大量重复的表达式来取消这些临时变量的也可以让代码复杂起来。

--

### 步骤5：继续弄乱变量名

```c
void _(int __, int ___, int ____)
{
    ((___ / __) <= 1) ? _(__,___+1,____) : !(___ % __) ? _(__,___+1,___ % __) :
    ((___ % __)==(___ / __) && !____) ? (printf("%d\n",(___ / __)),
    _(__,___+1,____)) : ((___ % __) > 1 && (___ % __) < (___ / __)) ?
    _(__,___+1,____ + !((___ / __) % (___ % __))) : (___ < __ * __) ?
    _(__,___+1,____) : 0;
}

int main()
{
    _(100,0,0);
}
```

Note:
我们知道，下划线是合法的变量名，所以，我们不妨用__，___，____来代替m，t，c。函数名也可以使用下划线来代替。

--

### 步骤6：移除常量

```c
void _(int __, int ___, int ____, int _____)
{
    ((___ / __) <= _____) ? _(__,___+_____,____,_____) : !(___ % __) ? _(__,___+_____,___ % __, _____) :
    ((___ % __)==(___ / __) && !____) ? (printf("%d\n",(___ / __)),
    _(__,___+_____,____,_____)) : ((___ % __) > _____ && (___ % __) < (___ / __)) ?
    _(__,___+_____,____ + !((___ / __) % (___ % __)),_____) : (___ < __ * __) ?
    _(__,___+_____,____,_____) : 0;
}

int main() {
    _(100,0,0,1);
}
```

Note:
在上面的程序中，还有一些常量，你可以通过增加一个宏定义，或是增加一个函数的形参来取代这一常量。
