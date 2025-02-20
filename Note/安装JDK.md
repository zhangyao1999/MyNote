- **PATH**是给操作系统识别的，比如在命令行中敲入java javac等命令时，系统会去PATH中去找路径下的exe 。
- **JAVA_HOME**时所有需要调用JDK的软件约定俗成的路径。
- **CLASSPATH**顾名思义为包路径，告诉Java在执行的时候，去哪里找到需要的包和类供程序使用，JDK版本大于1.5之后不需要了。
	- 我们经常见JAVA_HOME这个路径包含在PATH中是为了方便以后有更新或者切换JDK的时候不用改来改去，只改一处未知就可以了。
- 安装后直接使用java -version就可以查看java版本。11

- 变量名：**JAVA_HOME**
- 变量值：**C:\Program Files (x86)\Java\jdk1.8.0_91**        // 要根据自己的实际路径配置

- 变量名：**CLASSPATH**
- 变量值：**.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;**         //记得前面有个"."
- 变量名：**Path**
- 变量值：**%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;**
