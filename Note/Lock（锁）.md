JDK5.0开始，java提供了更强大的线程同步机制，通过显式定义同步锁对象来实现同步，同步锁使用Lock对象来充当。
java.util.concurrent.locks.Lock接口是控制多个线程对共享资源进行访问的工具。锁提供了对共享资源的独占访问，每次只能有一个线程对Lock对象加锁，线程开始访问共享资源之前应先获得Lock对象。
ReentrantLock类实现了Lock。可以显式的加锁，释放锁。
```java
import java.util.concurrent.locks.ReentrantLock;

public class StudyLock {
    public static void main(String[] args) {
        Window1 window11 = new Window1();
        Thread window1 = new Thread(window11);
        window1.setName("窗口1");
        Thread window2 = new Thread(window11);
        window2.setName("窗口2");
        Thread window3 = new Thread(window11);
        window3.setName("窗口3");
        window1.start();
        window2.start();
        window3.start();
    }

}

class Window1 implements Runnable {
    private static int num = 100;
    // 1.实例化lock 需要保证多个线程用的是同一个对象
    private ReentrantLock lock = new ReentrantLock();// true（先进先出） false 是否公平

    @Override
    public void run() {
        while (true) {
            try {
                // 2.调用lock方法
                lock.lock();
                if (num > 0) {
                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        throw new RuntimeException(e);
                    }
                    System.out.println(Thread.currentThread().getName() + "窗口卖了第" + num + "号票");
                    num--;
                } else {
                    System.out.println(Thread.currentThread().getName() + "窗口停止卖票");
                    break;
                }
            } finally {
                // 3.调用解锁方法
                lock.unlock();
            }
        }
    }
}

```

面试题：synchronized 和 lock 的异同
相同：都是解决现场安全问题
不同：synchronized 是隐式锁 机制在执行完相应的同步代码以后， 自动的释放同步监视器
		lock 是显式锁 需要手动的去启动同步 同时结束同步也需要手动的实现。jvm将花费更少的时间来调度线程，性能更好，并且具有更好的扩展性（提供更多的子类）。