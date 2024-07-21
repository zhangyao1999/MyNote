



### 关键字 final


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
