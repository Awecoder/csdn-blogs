## **http协议**
在浏览器的地址栏输入一个地址的时候，就能够访问服务器的某个页面。过程是两个应用程序之间的交互，一个应用程序是浏览器，另一个应用程序是服务器。

<font color = #0000ff size = 4>协议</font>就是不同的应用程序之间按照事先做好的约定进行的通信。

浏览器和WEB服务器之间，使用的就是一种叫做HTTP的协议。 这样是<font color = #0000ff size = 4>BS (Browser Server )架构模型</font>的基础.

http协议由请求和响应两种类型组成。
<font color = #0000ff size = 4></font>

## **调试工具**
利用火狐浏览器调试工具观察浏览器和服务器之间传输数据的具体内容。

- 安装火狐44.0
- 安装firebug：
菜单->Tools->Add-ons ->Install Add-on From File.

- 打开调试工具：F12
- 观察request response 请求响应
查看浏览器和服务器传输的协议内容


## **请求协议POST**
### 1 请求行 
### 2 请求头部
**请求头部信息**提供了如下信息: 
Host: 主机名
Use-Agent: 浏览器基本资料
Accept: 浏览器能够识别的响应类型
Accept-Language: 浏览器默认语言
Accept-Encoding: 浏览器能够识别的压缩方式
Referer: 来路页面， /addHero 这个路径是通过addHero.html这个页面跳转过来的。
Connecton：是否保持连接
### 3 请求数据
## **响应协议 response**
### 1 状态行
### 2 消息报头
消息报头中提供如下信息： 
Conent-Length: 表示长度
Content-Type: 内容格式
Date: 日期
Server: 服务器类型
### 3 响应正文

## **响应代码**
200	响应成功

301	表示客户端跳转，永久性的跳转
为了实现301跳转，在Servlet中应该使用如下代码：
response.setStatus(301);
response.setHeader("Location", "fail.html");

302	客户端跳转，临时性的跳转
在Servlet的代码实现要比301简单点，直接使用
response.sendRedirect("/listHero")

304	表示资源未被修改。
当不是第一次访问一个静态页面或者图片的时候，就会得到这么一个提示。这是服务端提示浏览器，这个资源没有发生改变，你直接使用上一次下载的就行了，不需要重新下载。 这样就节约了带宽，并且浏览器的加载速度也更快。

404	表示访问的页面不存在

500  表示服务端的错误
比如新增数据，服务器进行数据格式转换抛出异常。属于服务器问题