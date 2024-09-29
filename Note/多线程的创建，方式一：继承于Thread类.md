- 创建一个继承于Thread类的子类
- 重写run方法
	- 如果直接调用run 那么不会有新线程，只会在main线程内顺序执行。
- 实例化子类
- 调用start方法
	- 作用（启动线程 调用线程的run方法）
	- 如果同一个实例调用多次start 会报异常。一个实例只能调用一次start

```java
public class Test12 {  
    public static void main(String[] args) {  
        MyThread myThread = new MyThread();  
        myThread.start();  
        for (int i = 0; i < 100; i++) {  
            if (i % 2 == 0) {  
                System.out.println("Main Thread Print"+i);  
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
                System.out.println("new Thread Print"+i);  
            }  
        }  
    }  
}
```
这里俩个线程交替执行 打印混杂在一起

[[例题：多窗口卖票]]
[[Thread的匿名子类]]
