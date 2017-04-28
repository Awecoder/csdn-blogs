## Servlet 基础
Servlet 为创建基于 web 的应用程序提供了基于组件、独立于平台的方法，可以不受 CGI (通用网关接口Common Gateway Interface/CGI)程序的性能限制。

Servlet 有权限访问所有的 Java API，包括访问企业级数据库的 JDBC API。

Servlet 本身不能独立运行，需要在一个web应用中运行的。而一个web应用可以部署到Tomcat中。
## 项目搭建
我们使用eclipse EE版，结合Tomcat完成Java项目的创建
### 创建普通的Java项目
File->New->Other->Java->Java Project，创建好普通的Java项目
放在 e:\project\j2ee目录下
### 导入servlet-api.jar
servlet-api.jar 包位于 tomcat\lib\servlet-api.jar

java 项目导入jar包的方法：
右键点击项目 -> properties -> Java Build Path ->Libraries -> Add External JARs
![这里写图片描述](http://img.blog.csdn.net/20170407205117001?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### 编写HelloServlet
创建 HelloServlet，包名置空。

```
import java.io.IOException;
import java.util.Date;
 
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
 
public class HelloServlet extends HttpServlet{
 
    public void doGet(HttpServletRequest request, HttpServletResponse response){
         
        try {
            response.getWriter().println("<h1>Hello Servlet!</h1>");
            response.getWriter().println(new Date().toLocaleString());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }  
}
```
### 配置web.xml
在j2ee下创建目录web，接着再创建目录web/WEB-INF，然后在WEB-INF目录中创建 web.xml

web.xml提供路径与servlet的映射关系。把/hello这个路径，映射到 HelloServlet这个类上

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app>
 
    <servlet>
        <servlet-name>HelloServlet</servlet-name>
        <servlet-class>HelloServlet</servlet-class>
    </servlet>
 
    <servlet-mapping>
        <servlet-name>HelloServlet</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
 
</web-app>
```
### 指定项目输出到classes目录
项目右键->properties->Java Build Path->Source->右下角的 Brower-> 指定位置是 j2ee/web/WEB-INF/classes
### 配置tomcat的server.xml 中的context 标签

```
<Context path="/" docBase="e:\\project\\j2ee\\web" debug="0" reloadable="false" />
```
path="/" 就表示直接通过 http://127.0.0.1/hello 就可以访问网页
### 删除tomcat webapps下的ROOT目录
server.xml中的path 配置为 "/" 与 webapps下的ROOT目录冲突
### 重启tomcat，访问http://127.0.0.1/hello

```
Serlet类--服务器操作，从web读取数据（比如名称和密码）等
web.xml---建立servlet和Tomcat服务器的映射链接
login.xml---登录页面
```
## 获取参数
### 创建login.xml
在web目录下新建login.xml文件
action="login" 表单提交到login路径
method="post"  名称密码浏览器地址栏不可见。
```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>登录页面</title>
</head>
<body>
  
<form action="login" method="post">
账号: <input type="text" name="name"> <br>
密码: <input type="password" name="password"> <br>
<input type="submit" value="登录">
</form>
  
</body>
</html>
```
### LoginServlet类
因为浏览器中的form的method是post,所以LoginServlet需要提供一个doPost方法

```
import java.io.IOException;
 
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
  
public class LoginServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        String name = request.getParameter("name");
        String password = request.getParameter("password");
  
        System.out.println("name:" + name);
        System.out.println("password:" + password);
    }
}
```
### web.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app>   
    <servlet>
        <servlet-name>LoginServlet</servlet-name>
        <servlet-class>LoginServlet</servlet-class>
    </servlet>
 
    <servlet-mapping>
        <servlet-name>LoginServlet</servlet-name>
        <url-pattern>/login</url-pattern>
    </servlet-mapping>    
</web-app>
```
### 提交数据
重启Tomcat，访问页面

```
http://127.0.0.1/login.html
```
在Tomcat窗口，看到提交的账号、密码
## 服务器响应
### LoginServlet
```
import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class LoginServlet extends HttpServlet {

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		// 请求：浏览器--> 服务器
		String name = request.getParameter("name");   
		String password = request.getParameter("password");
			
		String html = null;
		
		if("admin".equals(name) && "123".equals(password))
			html ="<div style='color:green'>success</div>";
		else
			html ="<div style='color:red'>fail</div>";
		
		response.setContentType("text/html; charset=UTF-8");
		// 相应:服务器--> 浏览器
		PrintWriter pw = response.getWriter();  // 字符缓冲输出流
		pw.println(html);
	}	
}
```
## 实现过程
步骤 1 : login.html    
访问http://127.0.0.1/login.html，打开静态页面，通过form，以post的形式提交数据。

步骤 2 : /login路径
 上一步通过form，以post的形式提交数据 到/login路径。
 
步骤 3 : 找到对应的Servlet    
tomcat接受到新的请求：http://127.0.0.1/login（协议+主机名+路径/login）
接着到配置文件web.xml进行匹配，找到/login对应的Servlet类。

步骤 4 : 实例化Servlet对象    
Tomcat 定位到了LoginServlet后，发现并没有LoginServlet的实例存在，于是就调用LoginServlet的public无参的构造方法LoginServlet()实例化一个LoginServlet。当然也可以重写构造函数。

步骤 5 : 调用doGet或者doPost    
Tomcat等到servlet 实例后，根据页面login.html提交信息的时候带的method="post"，去调用对应的doPost方法。

步骤 6 : request获取参数    
流程进入doPost方法，获取账号密码信息

```
String name = request.getParameter("name");
```

步骤 7 : response设置响应 
创建html字符串，把html字符设置到response对象上。

```
String html = "<div style='color:green'>success</div>";
response.setContentType("text/html; charset=UTF-8");
PrintWriter pw = response.getWriter();
pw.println(html);
```

   
步骤 8 : tomcat把html传递给浏览器   
此时servlet框架工作完成，tomcat拿到被Servlet修改过的response，根据这个response生成html 字符串，然后再通过HTTP协议，这个html字符串，回发给浏览器，浏览器再根据HTTP协议获取这个html字符串，并渲染在界面上。

### doPost/doGet/service 区别
当浏览器使用get方式提交数据的时候，servlet需要提供doGet()方法
form默认的提交方式
如果通过一个超链访问某个地址
如果在地址栏直接输入某个地址
ajax指定使用get方式的时候

当浏览器使用post方式提交数据的时候，servlet需要提供doPost()方法
在form上显示设置 method="post"的时候
ajax指定post方式的时候

在执行doGet()或者doPost()之前，都会先执行service()，
由service()方法进行判断，到底该调用doGet()还是doPost()，
所以，直接重写service()方法，在其中提供相应的服务，就不用区分到底是get还是post。

## 中文编码相关
### 获取中文参数
1 告诉浏览器，等下发消息给服务器的时候，使用UTF-8编码
```
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
```


2 form的method修改为post

3 在servlet进行解码和编码

```
byte[] bytes=  name.getBytes("ISO-8859-1");
name = new String(bytes,"UTF-8");
```
先根据ISO-8859-1解码，然后用UTF-8编码。此时可以得到正确参数。


request.setCharacterEncoding("UTF-8"); 可以代替之前操作。
并且放在request.getParameter()之前。

### 返回中文响应

```
response.setContentType("text/html; charset=UTF-8");
```
## servlet 生命周期（5个步骤）
### 1 实例化
当web.xml中某路径/login触发时，路径对应的servlet会被调用，servlet被实例化。
只会执行一次。
### 2 初始化
LoginServlet 继承了HttpServlet，同时也继承了init(ServletConfig) 方法init初始化只执行一次。
### 3 提供服务
doGet/doPost/service()方法
### 4 销毁
1 关闭tomcat的时候 destroy()方法会被调用
2 该Servlet所在的web应用重新启动

```
<Context path="/" docBase="e:\\project\\j2ee\\web" debug="0" reloadable="false" />
```
如果把 reloadable="false" 改为reloadable="true" 就表示有任何类发生的更新，web应用会自动重启
### 5 被回收

