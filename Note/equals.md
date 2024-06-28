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