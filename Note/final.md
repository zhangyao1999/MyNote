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

[[final的使用]]
