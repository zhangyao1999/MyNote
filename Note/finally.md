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