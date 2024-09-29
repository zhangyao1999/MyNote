```java
new Thread("线程2"){  
    @Override  
    public void run() {  
        // 输出100以内的所有偶数  
        for (int i = 0; i < 100; i++) {  
            if (i % 2 == 0) {  
                System.out.println("匿名 Thread Print" + i);  
            }  
        }  
    }  
}.start();

```