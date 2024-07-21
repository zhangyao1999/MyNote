


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
