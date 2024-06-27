- 概念 所有类的父类或者间接父类
- 方法
	- clone
-------------------------------------------------------
参考帖子：[java.lang.Object.clone()解读 - zero516cn - 博客园 (cnblogs.com)](https://www.cnblogs.com/gw811/archive/2012/10/07/2712252.html)
**读源码可以知道**
1.clone是**native方法** 
2.clone被protected修饰符修饰，所有子类的都可以使用 。
3.clone返回一个object对象。

**浅层复制与深层复制概念：**

**浅层复制：** 被复制的对象的所有成员属性都有与原来的对象相同的值，而所有的对其他对象的引用仍然指向原来的对象。换言之，浅层复制仅仅复制所考虑的对象，而不复制它所引用的对象。（概念不好理解，请结合下文的示例去理解）

**深层复制：** 被复制对象的所有变量都含有与原来的对象相同的值，除去那些引用其他对象的变量。那些引用其他对象的变量将指向被复制过的新对象，而不是原有的那些被引用的对象。换言之，深层复制要复制的对象引用的对象都复制一遍。

**实现clone方法需要注意**
- 类想要用clone方法必须实现Cloneable接口 否则会抛出CloneNotSupportedException。
- java的clone是浅拷贝。
- clone被protected修饰符修饰,子类内部可以使用，重写需要修改为public 方便子类外部调用。

**深拷贝的俩个例子：**
- 手动拷贝 不推荐
- 序列化拷贝 ：把对象写到流中的过程是串行化(Serilization)过程，而把对象从流中读出来是并行化(Deserialization)过程。应当指出的是，写在流中的是对象的一个拷贝，而原来对象仍然存在JVM里面。  　　在Java语言里深层复制一个对象，常常可以先使对象实现Serializable接口，然后把对象（实际上只是对象的一个拷贝）写到一个流中，再从流中读出来，便可以重建对象。  　　这样做的前提是对象以及对象内部所有引用到的对象都是可串行化的，否则，就需要仔细考察那些不可串行化的对象是否设成transient，从而将之排除在复制过程之外。代码改进如下：
``` java
package org.example;
 
import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.io.Serializable;
 
public class Test {
    public static void main(String[] args) throws CloneNotSupportedException, IOException, ClassNotFoundException {
        Person p1 = new Person();
        p1.name = "张垚";
        p1.age = 12;
        House house = new House();
        house.setAddress("济南");
        house.setPort(123);
        p1.house = house;
        Person p2 = (Person) p1.clone();
        p2.getHouse().setPort(124);
        System.out.println(p2);
        System.out.println(p1);
        Person p3 = (Person) p1.deepClone();
        System.out.println(p3);
    }
 
}
 
class Person implements Cloneable, Serializable { // 不Cloneable 会报错 不Serializable无法序列化
    String name;
    int age;
 
    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", house=" + house +
                '}';
    }
 
    public String getName() {
        return name;
    }
 
    public void setName(String name) {
        this.name = name;
    }
 
    public int getAge() {
        return age;
    }
 
    public void setAge(int age) {
        this.age = age;
    }
 
    public House getHouse() {
        return house;
    }
 
    public void setHouse(House house) {
        this.house = house;
    }
 
    House house;
 
    @Override
    public Object clone() throws CloneNotSupportedException {
        Person clone = (Person) super.clone();
        House clone1 = (House) house.clone();
        clone.setHouse(clone1);// 实现深克隆
        return clone;
    }
 
    public Object deepClone() throws IOException, ClassNotFoundException {// 序列化实现深克隆
        ByteArrayOutputStream byteArrayOutputStream = new ByteArrayOutputStream();
        ObjectOutputStream objectOutputStream = new ObjectOutputStream(byteArrayOutputStream);
        objectOutputStream.writeObject(this);
 
        ByteArrayInputStream byteArrayInputStream = new ByteArrayInputStream(byteArrayOutputStream.toByteArray());
        ObjectInputStream objectInputStream = new ObjectInputStream(byteArrayInputStream);
        return objectInputStream.readObject();
 
    }
 
}
 
class Student implements Cloneable, Serializable {
    String major;
    int score;
}
 
class House implements Cloneable, Serializable {
    String address;
    int port;
 
    public String getAddress() {
        return address;
    }
 
    public void setAddress(String address) {
        this.address = address;
    }
 
    @Override
    public String toString() {
        return "House{" +
                "address='" + address + '\'' +
                ", port=" + port +
                '}';
    }
 
    public int getPort() {
        return port;
    }
 
    public void setPort(int port) {
        this.port = port;
    }
 
    @Override
    public Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
 
```



------------------------------

- equals

**源码**
```java
public boolean equals(Object obj) {  
    return (this == obj);  
}
```
可以看到，Object原生的equals的效果和== 是相同的。要正确的使用该方法需要重写。像String Date File 包装类等都重写了eqlals方法。

**== 和 equals 的区别**

在*基本数据类型*中: 比较的是数值是否相等。（byte short int long double float char 他们互相之间都可以使用== 除了boolean）
在*引用数据类型*中:比较的是地址值是否相等，即俩个引用是否指向同一个对象实例。


-------------------------------

- finalize

当对象即将进行垃圾回收时，将调用该方法。
与C++中的析构函数不是对应的。C++中的析构函数调用的时机是确定的，而java不确定。
[finalize的作用 - zhangniuniu - 博客园 (cnblogs.com)](https://www.cnblogs.com/zyy1688/p/10838581.html)

---------------
