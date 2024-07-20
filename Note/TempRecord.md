**单例模式常见例子**
数据库连接，配置文件读取，应用程序的日志写入，网站的计数器

### 代码块
作用：用来初始化类，对象
**使用**
- 如果被修饰，只能用static 。也就是说只有静态代码块和构造代码块（类中）和普通代码块（方法中）。

**静态代码块**
格式：在java类中，使用static修饰{}。只能调用静态的结构。
```java
static {  
    System.out.println("静态代码块");  
}
```
**执行时机**:静态代码块在类被加载的时候就运行了，而且只运行一次，并且优先于==各种代码块以及构造函数==。如果一个类中有多个静态代码块，会按照书写顺序依次执行。
**作用**:例如项目启动需要加载的配置文件等资源，可以放入静态代码块中。

**非静态代码块**
格式：在类中，使用{}声明。
```java
{  
    System.out.println("构造代码块");  
}
```
**执行时机**:　构造代码块在创建对象时被调用，每次创建对象都会调用一次，但是优先于构造函数执行。需要注意的是，听名字我们就知道，构造代码块不是优先于构造函数执行，而是依托于构造函数，也就是说，如果你不实例化对象，构造代码块是不会执行的。如果存在多个构造代码块，则执行顺序按照书写顺序依次执行。
**作用**:构造函数的作用类似，都能对对象进行初始化，并且只要创建一个对象，构造代码块都会执行一次。但是反过来，构造函数则不一定每个对象建立时都执行（多个构造函数情况下，建立对象时传入的参数不同则初始化使用对应的构造函数）。做诸如统计创建对象的次数等功能

**普通代码块**
　　普通代码块和构造代码块的区别是，构造代码块是在类中定义的，而普通代码块是在方法体中定义的。且普通代码块的执行顺序和书写顺序一致。

**执行顺序**
静态代码块>构造代码块>构造函数>普通代码块
**父类和子类执行顺序**
先父后子 静态代码块内容先执行，接着执行父类构造代码块和构造方法，然后执行子类构造代码块和构造方法。

### 关键字 final

**作用**：
被final修饰的类不可以被继承
被final修饰的方法不可以被重写
被final修饰的变量不可以被改变

重点是第三句：
final修饰基本数据类型，值不可变  
final修饰引用数据类型，地址不可变，变量指向对象的内容可变。
```java
{  
    final Object[] objects = new Object[1];  
    objects[0] = new Object();  
    objects=  new Object[1];  // 这里编译过不去
}
```

**另外**
1 被final修饰的方法，JVM会尝试为之寻求内联，这对于提升Java的效率是非常重要的。因此，假如能确定方法不会被继承，那么尽量将方法定义为final的，(现在的java版本已经优化了)

2 被final修饰的常量，在编译阶段会存入调用类的常量池中，

3 **final修饰一个成员变量（属性），必须要显示初始化。** 这里有两种初始化方式，一种是在变量声明的时候初始化；第二种方法是在声明变量的时候不赋初值，但是要在这个变量所在的类的所有的构造函数中(或者某个代码块中)对这个变量赋初值。

```java
public class Study {  
    public final String a;  
  
    public Study() {  
        a = "123";  
    }  
  
    public Study(String b) {  
        a = b;  
    }  
  
}
```

```java

public class Study {  
    public final String a;  
  
    {  
        a = "123";  
    }  
  
    public Study() {  
    }  
  
    public Study(String b) {  
    }  
  
}

```

进阶: 被final修饰的常量在编译阶段会被放入常量池中

- final是用于定义常量的, 定义常量的好处是: 不需要重复地创建相同的变量. 而常量池是Java的一项重要技术, 由final修饰的变量会在编译阶段放入到调用类的常量池中.
- 请看下面这段演示代码. 这个示例是专门为了演示而设计的, 希望能方便大家理解这个知识点.

```java
public static void main(String[] args) {
    int n1 = 2019;          //普通变量
    final int n2 = 2019;    //final修饰的变量

    String s = "20190522";  
    String s1 = n1 + "0522";	//拼接字符串"20190512"
    String s2 = n2 + "0522";	

    System.out.println(s == s1);	//false
    System.out.println(s == s2);	//true
}
```

> 首先要介绍一点: 整数-127-128是默认加载到常量池里的, 也就是说如果涉及到-127-128的整数操作, 默认在编译期就能确定整数的值. 所以这里我故意选用数字2019(大于128), 避免数字默认就存在常量池中.

- 上面的代码运作过程是这样的:
- 首先根据final修饰的常量会在编译期放到常量池的原则, n2会在编译期间放到常量池中.
- 然后s变量所对应的"20190522"字符串会放入到字符串常量池中, 并对外提供一个引用返回给s变量.
- 这时候拼接字符串s1, 由于n1对应的数据没有放入常量池中, 所以s1暂时无法拼接, 需要等程序加载运行时才能确定s1对应的值.
- 但在拼接s2的时候, 由于n2已经存在于常量池, 所以可以直接与"0522"拼接, 拼接出的结果是"20190522". 这时系统会查看字符串常量池, 发现已经存在字符串20190522, 所以直接返回20190522的引用. 所以s2和s指向的是同一个引用, 这个引用指向的是字符串常量池中的20190522.

- 当程序执行时, n1变量才有具体的指向.
- 当拼接s1的时候, 会创建一个新的String类型对象, 也就是说字符串常量池中的20190522会对外提供一个新的引用.
- 所以当s1与s用"=="判断时, 由于对应的引用不同, 会返回false. 而s2和s指向同一个引用, 返回true.

> 总结: 这个例子想说明的是: 由于被final修饰的常量会在编译期进入常量池, 如果有涉及到该常量的操作, 很有可能在编译期就已经完成.

### 抽象类和抽象方法

**概念**
首先了解抽象方法，`public abstract void open();`。 抽象方法只有声明，没有具体的实现。java规定：如果一个类有抽象方法，则这个类为抽象类。抽象类必须要用abstract修饰。
- 抽象类不可实例化

- 抽象方法只能是public或者protected。因为如果是private，子类无法继承，也就不能实现该方法。默认不写是public

- 子类若继承于一个抽象类，必须实现父类的全部抽象方法，除非自己也是抽象类（此时子类和父类的抽象方法不可以同名）。

- 抽象类也可以有具体的方法，也可以完全不包含抽象方法（那该类还有必要设置为抽象类么？）

**abstract**
- abstract不能与final并列修饰同一个类。
- abstract 不能与private、static、final或native并列修饰同一个方法。

**抽象类的匿名子类**

```java
public class Test12 {  
    public static void main(String[] args) {  
        useItem(new Item() {  
            @Override  
            public void method() {  
                System.out.println("抽象类的匿名子类对象");  
            }  
        });  
    }  
    public static void useItem(Item item){  
        item.method();  
    }  
}  
abstract class Item {  
    public abstract void method();  
}
```

**模板方法与设计模式**

功能的一部分是固定的，一部分是易变的，利用多态可以将固定通用的写在父类中，容易变的写在子类中实现。

```java
public class Test13 {  
    public static void main(String[] args) {  
        BankProcess bankProcess = new BankInput();  
        bankProcess.process();  
        BankProcess bankProcess2 = new BankOutPut();  
        bankProcess2.process();  
    }  
}  
  
abstract class BankProcess {  
    private void pre() {  
        System.out.println("取号");  
    }  
  
    private void after() {  
        System.out.println("反馈评分");  
    }  
  
    protected abstract void invoke(); // 钩子方法 挂住哪个子类执行哪个方法  
  
    public final void process() {  
        pre();  
        invoke();  
        after();  
    }  
}  
  
class BankInput extends BankProcess {  
  
    @Override  
    protected void invoke() {  
        System.out.println("存款");  
    }  
}  
  
class BankOutPut extends BankProcess {  
  
    @Override  
    protected void invoke() {  
        System.out.println("贷款");  
    }  
}

```

**接口**

继承是一个 “是不是” （is - a）的关系，而接口实现这是 “能不能”( like - a) 的关系。接口的本质是规范。将不同的类的相同的行为特征抽取出来。

**接口中的成员**

jdk1.7之前 只能有全局常量（public static final）和抽象方法(public abstract)
jdk1.8之后 除了上面以外，还能有静态方法，默认方法。。。

public static final 和public abstract 书写时可以省略。

接口不可以有构造器，当然也不能实例化。

子类实现接口必须实现全部抽象方法，除非该子类为抽象类。

接口和接口之前可以多继承。
但是类只能单继承多实现。
```java
interface AA {  
    void method1();  
}  
  
interface BB {  
    void method2();  
}  
  
interface CC extends AA, BB {  
  
}  
  
class DD implements CC {  
  
    @Override  
    public void method1() {  
  
    }  
  
    @Override  
    public void method2() {  
  
    }  
}

```

接口的匿名实现类
```java
new AA() {  
    @Override  
    public void method1() {  
        System.out.println("1");  
    }  
};
```

**接口的应用：代理模式**

代理模式是一种使用代理对象来执行目标对象的方法并在代理对象中增强目标对象方法的一种设计模式。

使用代理模式的原因有：

- 中介隔离作用：在某些情况下，一个客户类**不想或者不能直接引用**一个委托对象，而代理对象可以在客户类和委托对象之间起到**中介**的作用(代理类和委托类实现相同的接口)。以现实生活为例，经纪人就是明星的代理，外界可以通过联系经纪人来间接与明星沟通。
- 开放封闭原则：可以通过给代理类增加额外的功能来扩展委托类的功能，这样只需要修改代理类而不需要再修改委托类，符合开闭原则。代理类主要负责为委托类预处理消息、过滤消息、把消息转发给委托类，以及事后对返回结果的处理等。代理类本身并不真正实现服务，而是同过调用委托类的相关方法，来提供特定的服务。使用代理模式，可以在调用委托类业务功能的前后加入一些公共的服务(例如鉴权、计时、缓存、日志、事务处理等)，甚至修改委托类的业务功能。

代理可以分为静态代理和动态代理，前者更接近代理模式的本质。

- 静态代理是由程序员编写代理类的源码，再编译代理类。所谓静态也就是在程序运行前就已经存在代理类的字节码文件，代理类和委托类的关系在运行前就已确定。
- 动态代理是代理类的源码是在程序运行期间由编译器动态的生成(如JVM根据**反射**等机制生成代理类)。代理类和委托类的关系在程序运行时确定。

```java
public class Test16 {  
    public static void main(String[] args) {  
        manger manger = new manger(new RealStar());  
        manger.process();  
    }  
}  
  
interface Star {  
    void sing();  
  
    void dealAction();  
}  
  
class RealStar implements Star {  
  
    @Override  
    public void sing() {  
        System.out.println("明星唱歌");  
    }  
  
    @Override  
    public void dealAction() {  
  
    }  
}  
  
class manger implements Star {  
  
    private Star star;  
  
    public manger(Star star) {  
        this.star = star;  
    }  
  
    @Override  
    public void sing() {  
        System.out.println("经理人准备工作");  
        star.sing();  
        System.out.println("经理人收尾工作");  
    }  
  
    @Override  
    public void dealAction() {  
        System.out.println("经纪人处理活动");  
    }  
  
    public void process(){  
        sing();  
        dealAction();  
    }  
}

```
**工厂模式**

实现了创建者和调用者的分离，即将创建对象的具体过程屏蔽合理起来，达到提高灵活性的目的。

学完反射再写。

接口面试题：
类与接口同名参数

```java
public class Test18 {  
    public static void main(String[] args) {  
        new C().showX();  
    }  
}  
  
class A {  
    int x = 0;  
}  
interface B{  
    int x =2;  
}  
class C extends A implements B{  
    public void showX(){  
        System.out.println(super.x);  
        System.out.println(B.x);  
    }  
}
```
**java8提供的新特性**

- 接口中定义的静态方法，只能用过接口来调用。
- 通过实现类的对象，可以调用接口中的默认方法。如果实现类重写了接口中的默认方法，调用时，仍然调用的是重写以后的方法。
- 如果子类继承的父类和实现的接口中声明了同名同参数的方法，那么子类在没有重写此方法的情况下，默认调用的是父类中的同名同参数的方法。-类优先（仅针对方法，属性需要区分调用）
- 在子类中调用被父类，接口重写的方法 分别是`super.method();` `Interface.super.method();`
```
public class Test18 {  
    public static void main(String[] args) {  
        A.method1(); // 静态方法直接用接口调用  
        new B().method2(); // 默认方法使用实现类调用  
        //new B().method1(); // 报错  静态方法不能用实现类调用  
    }  
}  
interface A{  
    void method();  
    int X = 123;  
    // 静态方法和默认方法的public 都可以省略  
    public static void method1(){  
        System.out.println("静态方法");  
    }  
    public default void method2(){  
        System.out.println("默认方法");  
    }  
}  
class B implements A{  
    @Override  
    public void method() {  
        System.out.println("实现方法");  
    }  
}
```

**内部类**
内部类分为成员内部类（静态和非静态）和局部内部类（方法内 代码块内 构造器内）
```java
class AA {  
      
  
    class BB {  
  
    }  
  
    static class FF {  
  
    }  
  
    public void method() {  
        class CC {  
  
        }  
    }  
  
    {  
        class DD {  
  
        }  
    }  
  
    public AA() {  
        class EE {  
  
        }  
    }  
}
```

- 内部类的方法里边可以直接调用外部类的方法 同样适用于静态规则
	- 调用方式 `method()或者外部类名.this.method();`   属性也是一样
- 内部类可以被权限修饰符修饰。

**实例化内部类**

- 实例化静态内部类
	`AA.FF ff = new AA.FF();`

- 实例化非静态内部类
	`AA a = new AA();  AA.BB bb = a.new BB();`

**使用举例**
局部内部类：
```java
public class Study {  
    public Comparable getComparable (){  
        class MyComparable implements Comparable{  
  
            @Override  
            public int compareTo(Object o) {  
                return 0;  
            }  
        }  
        return new MyComparable();  
    }  
    public Comparable getComparable2 (){  
        return new Comparable(){  
  
            @Override  
            public int compareTo(Object o) {  
                return 0;  
            }  
        };  
    }  
}
```

```java
public class Study {  
   public void method (){  
       String name = "123";  
       class BB{  
           public void userName(){  
               System.out.println(name); // 局部内部类的方法中使用外层方法的局部变量 要求该局部变量必须是final的 jdk8可以省略 但实际也是final的  
           }  
       }  
   }  
}
```

**异常**

java语言中，将程序发送的不正常情况称为异常（语法错误和逻辑错误不是异常）
异常（Throwable）分为两类：
Error:
java虚拟机无法解决的严重问题，如jvm系统内部错误，资源耗尽等情况。StackOverflowError(方法递归容易导致) 和OOM（new 了一个很大的数组 堆溢出）。一般不编写针对性的问题处理。

Exception：其他编程错误或者外在的因素导致的一般性问题。

**异常的分类**
编译时异常(IOException ClassNotFountException)

运行时异常(RuntimeException)

**异常处理方式**
方式一：try catch finally
catch中的异常类型如果没有子父类关系，谁在上下无所谓，如果有则子类在上
finally 是一定会执行的 即使catch中有异常 return 或者try中有return  也还是会执行 且此处的return会覆盖前两处结构的return

```java
public class Test12 {  
    public static void main(String[] args) {  
        System.out.println(Method());   // 3
    }  
  
    static int Method() {  
        try {  
            int i = 1 / 0;  
            return 1;  
        } catch (Exception e) {  
            return 2;  
        } finally {  
            return 3;  
        }  
    }  
}
```
方式二：在方法签名处 throws + 异常类型
