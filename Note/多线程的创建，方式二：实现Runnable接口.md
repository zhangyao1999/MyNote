**步骤**
1. 创建一个实现了Runnable接口的类
2. 实现类的抽象方法 run()
3. 创建实现类的对象
4. 将此对象作为参数传递到Thread累的构造器中，创建Thread累的对象
5. 通过Thread类的对象调用start()方法

**源码解释**
为什么都是调用start 既可以支持方式一又可以支持方式二呢。答案在run的源码里
[[run]]

**举例**
```java
public class shixianRunnable {  
    public static void main(String[] args) {  
        Runnable runnable = new MyRunnable();  
        Thread thread = new Thread(runnable);  
        Thread thread2 = new Thread(runnable);  
        thread.start();  
        thread2.start();  
    }  
}  
class MyRunnable implements Runnable{  
    @Override  
    public void run() {  
        for (int i = 0; i < 100; i++) {  
            if(i%2==0){  
                System.out.println(Thread.currentThread().getName()+"   "+i);  
            }  
        }  
    }  
}

```
