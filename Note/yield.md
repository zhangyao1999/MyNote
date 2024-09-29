```java
class MyThread extends Thread {  
  
    @Override  
    public void run() {  
        // 输出100以内的所有偶数  
        for (int i = 0; i < 100; i++) {  
            if (i % 2 == 0) {  
                System.out.println(Thread.currentThread().getName() + i);  
            }  
            if (i % 20 == 0) {  
                Thread.yield();  // 这里指的是当前线程 
            }  
        }  
    }  
}

```
Thread.yield(); 静态方法在哪里调用就在哪个线程下生效。