**源码**

```java

/**  
 * If this thread was constructed using a separate * <code>Runnable</code> run object, then that * <code>Runnable</code> object's <code>run</code> method is called; * otherwise, this method does nothing and returns. * <p>  
 * Subclasses of <code>Thread</code> should override this method. * * @see     #start() * @see     #stop() * @see     #Thread(ThreadGroup, Runnable, String)  
 */@Override  
public void run() {  
    if (target != null) {  
        target.run();  
    }  
}

```
这里如果Thread的子类重写了run方法，就直接调用子类run 。而如果没有重写，Thread构造器又传入了Runnable的实现类，这里target就不为空，就会调用target的run方法。