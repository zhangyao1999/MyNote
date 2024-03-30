### 1 conf
#### 1.1修改localrespository
#### 1.2 修改中央仓库网址  
```xml
<mirror>

<id>alimaven</id>

<name>aliyun maven</name>

<url>http://maven.aliyun.com/nexus/content/groups/public/</url>

<mirrorOf>central</mirrorOf>

</mirror>
```
#### 1.3 默认使用1.8版本
```xml
    <profile>    
      <id>jdk-1.8</id>    
      <activation>    
     	  <activeByDefault>true</activeByDefault>    
      	<jdk>1.8</jdk>    
      </activation>    
      <properties>    
        <maven.compiler.source>1.8</maven.compiler.source>    
        <maven.compiler.target>1.8</maven.compiler.target>    
        <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>    
      </properties>    
    </profile>
```
#### 1.4 环境变量
需要依赖JAVA_HOME 正确配置
其次在PATH配置maven的环境变量