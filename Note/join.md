
```java
package org.example;  
  
public class Test12 {  
    public static void main(String[] args) throws InterruptedException {  
        MyThread myThread = new MyThread();  
        myThread.start();  
        Thread.currentThread().setName("主线程  ");  
        myThread.setName("线程1  ");  
        for (int i = 0; i < 100; i++) {  
            if (i % 2 == 0) {  
                System.out.println(Thread.currentThread().getName() + i);  
            }  
            if (i == 20) {  
                myThread.join();  // 在主线程调用分线程的join方法，会让主线程在打印到20的时候执行分线程，并且直到分线程执行完毕才会继续执行主线程。
            }  
        }  
    }  
}  
  
class MyThread extends Thread {  
  
    @Override  
    public void run() {  
        // 输出100以内的所有偶数  
        for (int i = 0; i < 100; i++) {  
            if (i % 2 == 0) {  
                System.out.println(Thread.currentThread().getName() + i);  
            }  
            if (i % 20 == 0) {  
                this.yield();  
            }  
        }  
    }  
}

```
非静态方法，必须得用其他线程的对象调用。