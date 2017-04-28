> request对象的类是HttpServletRequest

<font color=#0000ff size=4>requst是请求，浏览器端（B）到服务器端（S）的请求。</font>
例如：
```
protected void doPost(HttpServletRequest request, HttpServletResponse response){
...
}
```
---
## **request 常见方法**
request.**getRequestURL**(): 浏览器发出请求时的完整URL，包括协议 主机名 端口(如果有)" + 
request.**getRequestURI**(): 浏览器发出请求的资源名部分，去掉了协议和主机名" + 
request.**getQueryString**(): 请求行中的参数部分，只能显示以get方式发出的参数，post方式的看不到
request.**getRemoteAddr**(): 浏览器所处于的客户机的IP地址
request.**getRemoteHost**(): 浏览器所处于的客户机的主机名
request.**getRemotePort**(): 浏览器所处于的客户机使用的网络端口
request.**getLocalAddr**(): 服务器的IP地址
request.**getLocalName**(): 服务器的主机名
request.**getMethod**(): 得到客户机请求方式一般是GET或者POST

### servlet类
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
		
		// 打印到tomcat上
		System.out.println();
        System.out.println("浏览器发出请求时的完整URL，包括协议 主机名 端口(如果有): " + request.getRequestURL());
        System.out.println("浏览器发出请求的资源名部分，去掉了协议和主机名: " + request.getRequestURI());
        System.out.println("请求行中的参数部分: " + request.getQueryString());
        System.out.println("浏览器所处于的客户机的IP地址: " + request.getRemoteAddr());
        System.out.println("浏览器所处于的客户机的主机名: " + request.getRemoteHost());
        System.out.println("浏览器所处于的客户机使用的网络端口: " + request.getRemotePort());
        System.out.println("服务器的IP地址: " + request.getLocalAddr());
        System.out.println("服务器的主机名: " + request.getLocalName());
        System.out.println("得到客户机请求方式: " + request.getMethod());
		
		// 登录反馈	
		String html = null;		
		if("admin".equals(name) && "123".equals(password))
			html ="<div style='color:green'>success</div>";
		else
			html ="<div style='color:red'>fail</div>";
		
		response.setContentType("text/html; charset=UTF-8");
		// 响应:服务器--> 浏览器
		PrintWriter pw = response.getWriter();  // 字符缓冲输出流
		pw.println(html);
	}
}

```
### login.html

```
<!DOCTYPE html>
<html>
<head>
<!-- html5新写法 -->
<meta charset="UTF-8">
<!-- meta http-equiv="Content-Type" content="text/html,charset=UTF-8" 旧式写法 -->
<title>登录页面</title>
</head>

<body>
<form action="login" method="post">
账号：<input type="text" name="name"><br>
密码：<input type="password" name="password"><br>
<input type="submit" value="登录">
</form>

</body>
</html>
```
### web.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<!-- web.xml提供路径映射到servlet -->
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
访问127.0.0.1/login.html
![这里写图片描述](http://img.blog.csdn.net/20170408124222502?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

---

## **获取参数**
request.getParameter(): 是常见的方法，用于获取单值的参数
request.getParameterValues(): 用于获取具有多值得参数，比如注册的时候提交的爱好，可以使多选的。
request.getParameterMap(): 用于遍历所有的参数，并返回Map类型。

例：
### 一个注册页面 register.html
```
<!DOCTYPE html>
 
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
 
<form action="register" method="get">
    账号 ： <input type="text" name="name"> <br>
    爱好 ： LOL<input type="checkbox" name="hobits" value="lol"> 
        DOTA<input type="checkbox" name="hobits" value="dota"> <br>
       
         <input type="submit" value="注册">
</form>
```
### 服务端的 RegisterServlet

```
import java.io.IOException;
import java.util.Arrays;
import java.util.Map;
import java.util.Set;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class RegisterServlet extends HttpServlet {

	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		System.out.println("获取单值参数name:" + request.getParameter("name"));

		String[] hobits = request.getParameterValues("hobits");
		System.out.println("获取具有多值的参数hobits: " + Arrays.asList(hobits));

		System.out.println("通过 getParameterMap 遍历所有的参数： ");
		Map<String, String[]> parameters = request.getParameterMap();

		Set<String> paramNames = parameters.keySet();
		for (String param : paramNames) {
			String[] value = parameters.get(param);
			System.out.println(param + ":" + Arrays.asList(value));
		}
	}
}
```
### web.xml 映射关系

```
<?xml version="1.0" encoding="UTF-8"?>
<!-- web.xml提供路径映射到servlet -->
<web-app>

    <servlet  
    <servlet>
    	<servlet-name>RegisterServlet</servlet-name>
    	<servlet-class>RegisterServlet</servlet-class>
    </servlet>  
    
    <servlet-mapping>
    	<servlet-name>RegisterServlet</servlet-name>
    	<url-pattern>/register</url-pattern>
    </servlet-mapping>
 
</web-app>
```
访问127.0.0.1/register.html
![这里写图片描述](http://img.blog.csdn.net/20170408125329079?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![这里写图片描述](http://img.blog.csdn.net/20170408125341767?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)



访问：127.0.0.1/hello, 打印到tomcat上。

## **获取头信息**
request.getHeader() 获取浏览器传递过来的头信息。 
比如getHeader("user-agent") 可以获取浏览器的基本资料，这样就能判断是firefox、IE、chrome、或者是safari浏览器
request.getHeaderNames() 获取浏览器所有的头信息名称，根据头信息名称就能遍历出所有的头信息
访问HelloServlet获取如下头信息:
host: 主机地址
user-agent: 浏览器基本资料
accept: 表示浏览器接受的数据类型
accept-language: 表示浏览器接受的语言
accept-encoding: 表示浏览器接受的压缩方式，是压缩方式，并非编码
connection: 是否保持连接
cache-control: 缓存时限

```
import java.io.IOException;
import java.util.Date;
import java.util.Enumeration;

import javax.servlet.ServletConfig;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
 
public class HelloServlet extends HttpServlet{
    public void doGet(HttpServletRequest request, HttpServletResponse response){
    	
    	Enumeration<String> headerNames= request.getHeaderNames();
    	while(headerNames.hasMoreElements()){
    		String header = headerNames.nextElement();
    		String value = request.getHeader(header);
    		System.out.printf("%s\t%s%n",header,value);
    	}
         
        try {
            response.getWriter().println("<h1>Hello Servlet!</h1>");
            response.getWriter().println(new Date().toLocaleString());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

![这里写图片描述](http://img.blog.csdn.net/20170408144019180?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
## **服务端传参数**
setAttribute和getAttribute可以用来在进行服务端跳转的时候，在不同的Servlet之间进行数据共享