**java源码**
```java
public String toString() {  
    return getClass().getName() + "@" + Integer.toHexString(hashCode());  
}
```
可以看到输出类名+jvm中的虚拟地址值
我们可以重写该方法输出类中的属性。