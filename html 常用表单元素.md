接上一篇文章： http://blog.csdn.net/lizhongping00/article/details/69388403
## **表单元素**
### **文本框**
#### **文本框**
只能够输入一行 
```
<input type="text">
```
#### **设置文本框长度**
input的size属性
```
<input type="text" size="10">
```
#### **文本框初始值**
属性value`

```
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
</head>

<input type="text" value="请按规定输入">`
```
#### **有背景文字的文本框**
属性placeholder 是html5属性。

```
<input type="text" placeholder="请输入账号">`
```
### **密码框**
输入数据会自动显示为星号

```
<input type="password">
```
### **表单**
form 标签，用于向服务器提交数据，比如账号密码。
#### **表单**

```
<form action="http://xxxx/login.jsp">
账号：<input type="text" name="name"> <br/>
密码：<input type="password" name="password" > <br/>
<input type="submit" value="登陆">
</form>
```

![这里写图片描述](http://img.blog.csdn.net/20170406210746473?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
#### **method="get"**
method="get" 提交数据（常用）
如果form元素没有提供method属性，**默认就是get方式提交数据** 
get方式的一个特点就是，可以在浏览器的地址栏看到提交的参数，**即便是密码也看得到**

```
?name=123456&password=123
```

```
<form method="get" action="http://xxxx/login.jsp">
账号：<input type="text" name="name"> <br/>
密码：<input type="password" name="password" > <br/>
<input type="submit" value="登陆">
</form>
```
#### **method="post"**
使用method="post" 也可以提交数据 
**post不会在地址栏显示提交的参数** 
如果要提交二进制数据，比如上传文件，必须采用post方式

```
<form method="post" action="http://xxxx/login.jsp">
账号：<input type="text" name="name"> <br/>
密码：<input type="password" name="password" > <br/>
<input type="submit" value="登陆">
</form>
```
#### **get 和 post 区别**
get和post的区别 
 <font color=#0000ff size=4>get</font>
是form默认的提交方式 
如果通过一个超链访问某个地址，是get方式 
如果在地址栏直接输入某个地址，是get方式 
提交数据会在浏览器显示出来 
不可以用于提交二进制数据，比如上传文件 
<font color=#0000ff size=4>post</font>
必须在form上通过 method="post" 显示指定 
提交数据不会在浏览器显示出来 
可以用于提交二进制数据，比如上传文件

### 单选框

```
<input type="radio">  表示单选框
```

#### 单选框
两个单选，都可以同时选中。
```
路飞 <input type="radio">
艾斯 <input type="radio">
```
#### 默认选中
属性checked
```
路飞 <input type="radio" checked="checked">
```
#### 分组
分组：多个单选框在同一个分组中，同一个时间，只能选中一个单选框。
设置name属性相同。

```
<p>最近在学啥</p>
Java<input type="radio" name="activity" value="java"> <br/>
JS<input type="radio" name="activity" value="JS"> <br/>
Python<input type="radio" name="activity" value="python"> <br/>
```
### 复选框

```
<input type="checkbox">
```

#### 复选框

```
<p>最近在学啥</p>
Java<input type="checkbox" name="activity" value="java" checked="checked"> <br/>
JS<input type="checkbox" name="activity" value="JS"> <br/>
Python<input type="checkbox" name="activity" value="python"> <br/>
```
### 下拉列表

```
<select> 配合<option>使用
```
#### 下拉列表

```
<select >
 <option >路飞</option>
 <option >艾斯</option>
 <option >萨博</option>
</select>
```

#### 设置高度
size属性

```
<select size="2">
 <option >路飞</option>
 <option >艾斯</option>
 <option >萨博</option>
</select>
```

#### 设置多选
multiple 属性
```
<select size="3" multiple="multiple">
 <option >路飞</option>
 <option >艾斯</option>
 <option >萨博</option>
</select>
```

#### 默认选中
selected属性

```
<select size="2" multiple="multiple">
 <option >路飞</option>
 <option >艾斯</option>
 <option selected="selected">萨博</option>
</select>
```
### 文本域

```
<textarea> 不同于文本框，文本域可以有多行，并且可以有滚动条。
```
#### 文本域

```
<textarea>路飞
艾斯
萨博
</textarea>
```
#### 设置宽度和行数
使用属性 cols 和 rows

```
<textarea cols="30" rows="8">路飞
艾斯
萨博
</textarea>
```
![这里写图片描述](http://img.blog.csdn.net/20170406220608132?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
### 普通按钮

```
<input type="button">
```
#### 普通按钮

```
<input type="button" value="我是按钮">
```
#### 普通按钮不具备form 提交效果
### 提交按钮

```
<input type="submit">
```
例：

```
<form action="/study/login.jsp" method="post">
账号：<input type="text" name="name"><br/>
密码：<input type="text" name="password"><br/>
<input type="submit" value="登录">
</form>
```
### 重置按钮

```
<input type="reset">
```
例

```
<form action="/study/login.jsp" method="post">
账号：<input type="text" name="name"><br/>
密码：<input type="text" name="password"><br/>
<input type="submit" value="登录">
<input type="reset" value="重置">
</form>
```
### 图像提交

```
<input type="image">
```
例

```
<form action="/study/login.jsp" method="post">
账号：<input type="text" name="name"><br/>
密码：<input type="text" name="password"><br/>
<br/>
<input type="image" src="http://p3.qhmsg.com/dr/270_500_/t0115d5c992be197524.png">
</form>
```
![这里写图片描述](http://img.blog.csdn.net/20170406222206604?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### 按钮

```
button 标签
与<input type="button">不同，button标签功能更丰富
```
#### 文字按钮

```
<button>路飞</botton>
```
#### 图片按钮

```
<button><img src="http://p3.qhmsg.com/dr/270_500_/t0115d5c992be197524.png"/></botton>
```
#### 提交按钮
除ie外，button的type默认为submit。
```
<form action="/study/login.jsp">
账号：<input type="text" name="name"><br/>
密码：<input type="password" name="password"><br/>

<button type="submit">登录</button>
</form>
```
### 练习

```
<html>

<head>
<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
</head>
<body>

<table width="100%">
<tr>
  <td align="right"><font color="red">*</font>用户名：</td>
  <td><input type="text" size="30"/><font color="red"> 用户名不得小于3个字符</font></td>
</tr>


<tr>
  <td align="right"><font color=#ff0000>*</font>密码：</td>
  <td><input type="text" size="30"/></td>
</tr>
<tr>
  <td align="right"><font color=#ff0000>*</font>Email：</td>
  <td><input type="text" size="30"/></td>
</tr>
<tr>
  <td align="right"><font color=#ff0000>*</font>真实姓名：</td>
  <td><input type="text" size="30"/></td>
</tr>
<tr>
  <td align="right"><font color=#ff0000>*</font>性别：</td>
  <td>
	<select size="1">
		<option selected="selected">男</option>
		<option>女</option>
	</select>
  </td>
</tr>
<tr>
  <td align="right"><font color=#ff0000>*</font>生日：</td>
  <td>
  <select name="select">
      <option>2017</option>
      <option>2016</option>
      <option>2015</option>
      <option>2014</option>
      <option>2013</option> 	  	  	  	  	  	  	  
    </select>
    <select name="select2">
      <option>1</option>
      <option>2</option>
      <option>...</option>
      <option>12</option>				
    </select>
    <select name="select3">
      <option>1</option>
      <option>2</option>
      <option>...</option>
      <option>31</option>						
    </select>
	</td>
</tr>


 <tr>
    <td align="right"><font color="#FF0000">*</font>居住地：</td>
    <td><select name="select4">
      <option>辽宁省</option>
    </select>
    <select name="select5">
      <option>沈阳市</option>
    </select> <select name="select6">
      <option>和平区</option>
    </select></td>
</tr>

<tr>
  <td align="right"><font color=#ff0000>*</font>手机：</td>
  <td><input type="text" size="30"/></td>
</tr>
  
<tr>
  <td align="right"></td>
  <td><font color=#0000ff size="-2">请输入准确信息</font></td>
</tr>

</table>
</body>
</html>
```
效果
![这里写图片描述](http://img.blog.csdn.net/20170407095747135?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)