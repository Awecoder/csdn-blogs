## **Tomcat**
Tomcat是常见的免费 web服务器。能够不依赖其它插件，独立提供web服务的效果。

### **不使用tomcat访问html**
可以在浏览器地址里使用

```
file:/C:/HelloWorld.java
```
以<font color = #0000ff size = 3>本地文件形式</font>打开。

而上网用的html网址http://12306.cn/xxxx形式，因为有web服务器的存在。

### **启动Tomcat**
下载[Tomcat](http://tomcat.apache.org/download-70.cgi)，解压缩到某一个盘。
运行E:\Javalearn\tomcat\bin 中的批处理文件startup.bat.
![这里写图片描述](http://img.blog.csdn.net/20170405151357671?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### **部署网页**
部署一张图片s.jpeg，把s.jpeg复制到E:\Javalearn\tomcat\webapps\ROOT目录下，
访问http://127.0.0.1:8080/s.jpeg

8080是tomcat默认使用的端口号
## **Tomcat 可能出现的问题**
### **1 JAVA_HOME问题**
Tomcat本身是JAVA程序，必须要有JDK才可以执行，所以必须配置JAVA_HOME。
### **2 CATALINA_HOME未设置问题**
分析：Tomcat执行必须依赖CATALINA_HOME或者CATALINA_BASE这两个环境变量。 如果没有在环境变量里配置过，那么会自动采用bin目录的父目录作为CATALINA_HOME和CATALINA_BASE。 如果配置了，而所配置的地方又不是正确的TOMCAT目录，那么就会出现这个错误。
解决：
1. 在环境变量中删除CATALINA_HOME,CATALINA_BASE的配置，记得不仅要检查环境变量，还要检查用户变量。
2. 或者把CATALINA_HOME设置为正确的TOMCAT目录。
### **3 端口冲突问题**
现象：Address already in use: JVM_Bind <null>:80，即表示端口被占用。

日志查看：在TOMCAT目录下的logs目录里，会有一个日志文件：catalina.yyyy-mm-dd.log（当天时间），在这个日志文件里会记载一样的错误:Address already in use: JVM_Bind <null>:80。即表明80端口被占用了。

分析：端口是独占式的，一旦一个程序占用了这个端口，其他程序就不能够再去占用它了。而80端口，有可能是被已经存在的Tomcat占用了，也有可能是被其他不知名的软件占用了，比如Apache,IIS,Oracle等等。
### **4 启动startup.bat报错**
现象：启动startup.bat就会报一大堆错误
检验：打开tomcat/logs目录里的localhost.yyyy-mm-dd.log文件，发现大量的报错信息。
分析：当server.xml， web.xml配置错误的时候，就会将错误信息输出到localhost.yyyy-mm-dd.log文件中。
### **5 Error FilterStart**
现象：404错误，明明有文件，但是就是不能访问。
检验：这个严格地说，也是配置失败，但是tomcat不会大量报错，只会偷偷地来这么一句： startup failed dut to previous errors。
分析：过滤器启动失败就会报这个错。
解决：同样的，过滤器启动失败原因也是多种多样，好在它都会把具体错误信息输出到localhost.yyyy-mm-dd.log
### 6 持久化异常
Tomcat启动的时候会报一个Exception loading sessions from persistent storage异常

该问题的原因是tomcat的session持久化机制引起的，tomcat这个功能本身的用意在于重启tomcat后保存之前的session，Tomcat会把session持久化在%TOMCAT%/work/Catalina/localhost/session.ser 这个文件里。 但是因为tomcat非正常关闭，所以这个文件正确的结束(无EOF标记)

<font color = #0000ff size = 4>解决办法治标</font>： 只需要删除 session.ser文件即可。

<font color = #0000ff size = 4>解决办法治本</font>：关闭tomcat的持久化功能，就能一劳永逸的解决这个问题。具体为修改conf下的server.xml文件。在项目的context间加入一句代码

```
<Context path="/" docBase="D:\\project\\j2ee\\web" debug="0" reloadable="false" >
    <Manager className="org.apache.catalina.session.PersistentManager" saveOnRestart="false"/>
</Context>
```

<font color = #0000ff size = 4>重启tomcat！！</font>

## **修改端口**
### **server.xml**
tomcat的端口配置相关信息在 server.xml中
E:\Javalearn\tomcat\conf\server.xml文件中找到8080端口
```
<Connector port="8080" protocol="HTTP/1.1"
          connectionTimeout="20000"
          redirectPort="8543" />
```
使用的是8080端口，把它修改为80，保存。

<font color = #0000ff size = 4>重启Tomcat，运行startup.bat !!</font>
### **80 端口**
此时，可以通过http://127.0.0.1/s.jpeg访问网页。

80端口是web 服务默认的端口号，所以不需要显式的写端口号。
## **端口被占用**
### **1 查看80端口**

```
netstat -ano | findstr "80"
```
查看 端口号包含"80"的占用情况
查询结果找到 80，8009，8005 （这三个都包含80）。 
对应的pid(process id) 进程id 是33468
![这里写图片描述](http://img.blog.csdn.net/20170405173148301?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### **2 根据pid（进程id）查询对应的应用程序**

```
tasklist | findstr "33468"
```
![这里写图片描述](http://img.blog.csdn.net/20170405173606185?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### **3 根据名称结束该程序**

```
taskkill /f /t /im java.exe
```

