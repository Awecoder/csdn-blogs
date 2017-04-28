>MVC 模式代表 Model-View-Controller（模型-视图-控制器） 模式，用于应用程序的分层开发。
## **MVC模式**
### **servlet缺陷**
servlet 操作需要准备数据，还要准备html，代码可读性差，不易维护。
参考
http://blog.csdn.net/lizhongping00/article/details/69802599

### **jsp缺陷**
在jsp中编写Java代码不如在servlet中方便。


### **结合servlet 和 jsp**
（1） HeroEditServlet.java
只用来从数据库中查询Hero对象，然后跳转到JSP 页面。

```
package servlet;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import enity.Hero;
import dao.HeroDAO;

public class HeroEditServlet extends HttpServlet {

	protected void service(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

		// 根据跳转，服务器获取参数id，根据id从数据库中查找到hero实例。
		int id = Integer.parseInt(request.getParameter("id"));
		Hero hero = new HeroDAO().get(id);
		request.setAttribute("hero", hero);
		request.getRequestDispatcher("editHero.jsp").forward(request, response);
	}
}
```
（2）editHero.jsp
服务端跳转到 editHero.jsp，因为是服务端跳转，都属于同一次请求。
jsp文件使用html编写。
editHero.jsp： 不做查询数据库的事情，直接获取从HeroEditServlet传过来的Hero对象，通过EL表达式把request的Hero显示出来。
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" import="java.util.*,bean.*,java.sql.*"%>
 
<form action='updatehero' method='post'>
    名字：<input type='text' name='name' value='${hero.name}'> <br>
    血量：<input type='text' name='hp' value='${hero.hp}'> <br>
    伤害：<input type='text' name='damage' value='${hero.damage}'> <br>
    <input type='hidden' name='id' value='${hero.id}'>
    <input type='submit' value='更新'>
</form>
```
### **MVC 设计模式**
M 代表 模型（model）：模型就是数据，就是dao，bean；
V 代表 视图（view）：视图就是网页，JSP，用来展示模型中的数据；
C 代表 控制器（controller）：控制器用来把不同的数据，显示在不同的视图上。

<font color=#0000ff>控制器的作用就是把不同的数据（Model），显示在不同的视图（View）上。</font>

本例中，servlet 作为控制器，把hero对象，显示在JSP上。
![这里写图片描述](http://img.blog.csdn.net/20170411212622912?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

## **servlet查询修改为MVC模式**
对servlet 数据库操作（查询）进行修改
### 对HeroListServlet进行修改
获取到数据后，request.setAttribute("heros", heros); 跳转到listHero.jsp

```
package servlet;
 
import java.io.IOException;
import java.util.List;
 
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
 
import enity.Hero;
import dao.HeroDAO;
 
public class HeroListServlet extends HttpServlet {
 
    protected void service(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html; charset=UTF-8");
         
        List<Hero> heros = new HeroDAO().list();
        
        request.setAttribute("heros", heros);
        request.getRequestDispatcher("listHero.jsp").forward(request, response);
 
    }
}
```
### listHero.jsp
jsp是view层，用于数据的显示。
首先设计表头，使用jstl循环读取数据，并添加超链接。
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8" import="java.util.*" %>
	
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>

<table align='center' border='1' cellspacing='0'>
	<tr>
		<td>id</td>
		<td>name</td>
		<td>hp</td>
		<td>damage</td>
		<td>edit</td>
		<td>delete</td>
	</tr>
	<c:forEach items="${heros }" var="hero" varStatus="st">
		<tr>
			<td>${hero.id }</td>
			<td>${hero.name }</td>
			<td>${hero.hp }</td>
			<td>${hero.damage }</td>
			<td><a href="edithero?id=${hero.id }">edit</a></td>
			<td><a href="deletehero?id=${hero.id }">delete</a></td>
		</tr>
	</c:forEach>
</table>
```
## 分页技术--MVC实现
分页技术是指一次只显示数据库的部分数据。并通过“下一页”、“最后一页”等翻页操作实现。

### DAO准备
http://blog.csdn.net/lizhongping00/article/details/69802599


### HeroListServlet实现

```
package servlet;

import java.io.IOException;
import java.util.List;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import enity.Hero;
import dao.HeroDAO;

public class HeroListServlet extends HttpServlet {

	protected void service(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		response.setContentType("text/html; charset=UTF-8");

		int start = 0;
		int count = 5;

		try {
			start = Integer.parseInt(request.getParameter("start"));
		} catch (NumberFormatException e) {
			// 当浏览器没有传参数start时
		}

		// 后一页
		int next = start + count;
		// 前一页
		int pre = start - count;

		// 最后一页
		int total = new HeroDAO().getTotal();
		int last;
		if (0 == total % count)
			// 总数为50个，则最后一页从45开始
			last = total - count;
		else
			// 总数为51个，则最后一页从50开始
			last = total - total % count;

		// 边界处理
		// 如果pre是负数，使用0
		pre = pre < 0 ? 0 : pre;
		// 如果next大于last，next等于last
		next = next > last ? last : next;

		request.setAttribute("next", next);
		request.setAttribute("pre", pre);
		request.setAttribute("last", last);

		List<Hero> heros = new HeroDAO().list(start, count);

		request.setAttribute("heros", heros);
		request.getRequestDispatcher("listHero.jsp").forward(request, response);

	}
}
```
### listHero.jsp

```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8" import="java.util.*" %>
	
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>

<table align='center' border='1' cellspacing='0'>
	<tr>
		<td>id</td>
		<td>name</td>
		<td>hp</td>
		<td>damage</td>
		<td>edit</td>
		<td>delete</td>
	</tr>
	<c:forEach items="${heros }" var="hero" varStatus="st">
		<tr>
			<td>${hero.id }</td>
			<td>${hero.name }</td>
			<td>${hero.hp }</td>
			<td>${hero.damage }</td>
			<td><a href="edithero?id=${hero.id }">edit</a></td>
			<td><a href="deletehero?id=${hero.id }">delete</a></td>
		</tr>
	</c:forEach>
	
	<!-- 分页标签 -->
	<tr>
		<td colspan="6" align="center">
			<a href="?start=0">[首页]</a>
			<a href="?start=${pre }">[上一页]</a>
			<a href="?start=${next }">[下一页]</a>
			<a href="?start=${last }">[末页]</a>
		</td>
	</tr>
</table>

```
![这里写图片描述](http://img.blog.csdn.net/20170411225140803?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### 使用BootStrap

```
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" import="java.util.*"%>
<!DOCTYPE html>
<script src="http://how2j.cn/study/js/jquery/2.0.0/jquery.min.js"></script>
<link href="http://how2j.cn/study/css/bootstrap/3.3.6/bootstrap.min.css" rel="stylesheet">
<script src="http://how2j.cn/study/js/bootstrap/3.3.6/bootstrap.min.js"></script>
     
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
 
<script>
$(function(){
    $("a").addClass("btn btn-default btn-xs");
     
});
 
</script> 
<table style="width:500px; margin:44px auto" class="table table-striped table-bordered table-hover  table-condensed" align='center' border='1' cellspacing='0'>
    <tr>
        <td>id</td>
        <td>name</td>
        <td>hp</td>
        <td>damage</td>
        <td>edit</td>
        <td>delete</td>
    </tr>
    <c:forEach items="${heros}" var="hero" varStatus="st">
        <tr>
            <td>${hero.id}</td>
            <td>${hero.name}</td>
            <td>${hero.hp}</td>
            <td>${hero.damage}</td>
            <td><a href="edithero?id=${hero.id}">编辑</a></td>
            <td><a href="deletehero?id=${hero.id}">删除</a></td>
        </tr>
    </c:forEach>
 
</table>
        <nav>
          <ul class="pager">
 
            <li><a href="?start=0">首  页</a></li>
            <li><a href="?start=${pre}">上一页</a></li>
            <li><a href="?start=${next}">下一页</a></li>
            <li><a href="?start=${last}">末  页</a></li>
          </ul>            
        </nav>
```
![这里写图片描述](http://img.blog.csdn.net/20170412090230048?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

## 用户登录
### 修改LoginServlet, 将验证成功的用户加入到session
验证成功跳转，不成功重新登录
```
import java.io.IOException;

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
		
		if("admin".equals(name) && "123".equals(password)){
			// 将用户名以“userName”放进session
			request.getSession().setAttribute("userName", name);
			// 客户端跳转到listhero
			response.sendRedirect("listhero");
		}		
		else
			// 客户端跳转
			response.sendRedirect("login.html");
	}	
}
```
##  在HeroListServlet中判断session中是否有数据

```
package servlet;

import java.io.IOException;
import java.util.List;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import enity.Hero;
import dao.HeroDAO;

public class HeroListServlet extends HttpServlet {

	protected void service(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		response.setContentType("text/html; charset=UTF-8");
		
		// 从session中取出userName，如果是空表示用户没有登录。客户端跳转login.html，让用户重新登录。
		// 如果登录超出30分钟，session会过期。（Tomcat的默认设置）
		String userName = (String) request.getSession().getAttribute("userName");
		if(null == userName){
			response.sendRedirect("login.html");
			return;
		}

		int start = 0;
		int count = 5;

		try {
			start = Integer.parseInt(request.getParameter("start"));
		} catch (NumberFormatException e) {
			// 当浏览器没有传参数start时
		}

		// 后一页
		int next = start + count;
		// 前一页
		int pre = start - count;

		// 最后一页
		int total = new HeroDAO().getTotal();
		int last;
		if (0 == total % count)
			// 总数为50个，则最后一页从45开始
			last = total - count;
		else
			// 总数为51个，则最后一页从50开始
			last = total - total % count;

		// 边界处理
		// 如果pre是负数，使用0
		pre = pre < 0 ? 0 : pre;
		// 如果next大于last，next等于last
		next = next > last ? last : next;

		request.setAttribute("next", next);
		request.setAttribute("pre", pre);
		request.setAttribute("last", last);

		List<Hero> heros = new HeroDAO().list(start, count);
		request.setAttribute("heros", heros);
		request.getRequestDispatcher("listHero.jsp").forward(request, response);

	}
}
```

