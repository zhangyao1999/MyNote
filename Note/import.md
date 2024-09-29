- 可以使用 * 省略 （* 只能省略类 不能省略子包）
- 不同包下同名的类要同时使用，至少有一个需要以全类名的方式显示。
- import static 如下  import static 可以导入类下的静态结构。可以省略类名
```java  
import static java.lang.System.*;
//import static java.lang.System.out;
  
public class Test1 {  
public static void main(String[] args) {  
	out.println("123");  
}  
}
```