## html

### 开发

文本文档.html

```
<html>
  <body>
    <p>Hello World</p>
  </body>
</html>
```
### 中文乱码问题
使用GB2312或UTF-8
```
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
</head> 
<p>中文</p>
```
### 标签
HTML是由一套标记标签 （markup tag）组成，通常就叫标签 
标签由开始标签和结束标签组成。
### 元素
一个完整的HTML文件，应该至少包含html元素，body元素，以及里面的内容

```
<html>
 <body>
   <h1>标题</h1>   
 </body>
</html>
```
目前，元素不完整，也可正常显示

特殊元素

```
<br/>  换行
<hr/>  水平线，有渲染效果，但是没有文本内容
```
### 属性
属性用来修饰标签的 ，比如要设置一个标题居中。 

```
<h1 >未设置居中的标题</h1>
 
<h1 align="center">居中标题</h1>
```
align 是 属性名
center 是 属性值，需要用<font color = #0000ff>双引号</font>括起来
### 注释

```
<!-- 我是注释 -->
```
## 基本元素1
### 标题
标题会自动粗体，大写其中的内容，并且带有换行效果。

```
<h1>标题1</h1>
<h2>标题2</h2>
<h3>标题3</h3>
<h4>标题4</h4>
<h5>标题5</h5>
```
### 段落
在p标签中的文本会自动换行，不在p标签中的，不会自动换行。

```
段落1
<p>段落2</p>
```
### 粗体
**b**是bold的缩写，仅仅表示该文本是粗体的，并不暗示这段文字的重要性；

```
<b>b标签粗体效果</b>
```

**strong**虽然也是粗体，但是更多的是强调语义上的加重，提醒用户该文本的重要性。 在SEO（搜素引擎优化）的时候，也更加容易帮助用户找到重点的内容

```
<strong>strong标签粗体效果</strong>
```
### 斜体
i是italic的缩写，仅仅表示该文本是斜体的，并不暗示这段文字的重要性

```
<i>i标签斜体效果</i>
```

em 是 Emphasized的缩写，虽然也是斜体，但是更多的是强调语义上的加重，提醒用户该文本的重要性。 常常用于引入新的术语的时候使用。

```
<em>em标签斜体效果</em>
```
粗体斜体嵌套

```
<strong><i>html学习</i></strong>
```
<strong><i>html学习</i></strong>
### 预格式--显示代码

```
<p>这里是没有用预格式的情况：</p>
 
public class HelloWorld {
 
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
 
<br/>
<p>使用预格式的情况:</p>
<pre>
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
</pre>
```
### 删除元素

```
<p>无删除效果</p>
<del>del标签删除效果</del>
<br/>
<s>s标签删除效果，但是不建议使用</s>
```
<del>del标签删除效果</del>
### 下划线

```
<ins>ins标签下划线效果</ins> 
<br/>
<u>u标签下划线效果，但是不建议使用</u>
```
<ins>使用ins标签实现的下划线效果</ins> 
### 练习案例
```
<html>
<body>
<head>
<meta http-equiv="Content-Type" content = "text/html;charset=UTF-8">
</head>
<h1>
英雄联盟（电子竞技类游戏）
</h1>
<p>
<strong>《英雄联盟》</strong>（简称lol）是由美国<em>Riot Games</em>开发，中国大陆地区由腾讯游戏运营的网络游戏。
</p>
<p>
<strong>《英雄联盟》</strong>即时战略，团队作战。[<ins>1</ins>]
</p>
<p>
官方数据最大同时在线已突破<del>750</del> 900万。 [<ins>2</ins>]
</p>	
</body>
</html>
```

<html>
<body>
<head>
<meta http-equiv="Content-Type" content = "text/html;charset=UTF-8">
</head>
<h1>
英雄联盟（电子竞技类游戏）
</h1>
<p>
<strong>《英雄联盟》</strong>（简称lol）是由美国<em>Riot Games</em>开发，中国大陆地区由腾讯游戏运营的网络游戏。
</p>
<p>
<strong>《英雄联盟》</strong>即时战略，团队作战。[<ins>1</ins>]
</p>
<p>
官方数据最大同时在线已突破<del>750</del> 900万。 [<ins>2</ins>]
</p>	
</body>
</html>

## 基本元素2
### 图像
#### 互联网图像
```
<img src="http://img1.niutuku.com/hd/1308/32/32-niutuku.com-252068.jpg"/>
```

<img src="http://img1.niutuku.com/hd/1308/32/32-niutuku.com-252068.jpg"/>

#### 同级目录图像
本地文件需将图片放到同一个目录下

```
<img src="example.png"/>
```
#### 上级目录图像
..	表示上级
```
<img src="../example.png"/>
```
#### 其它目录图像--加绝对路径
绝对路径  file://

```
<img src="file://c:/example.png"/>
```
#### 设置图像大小
放大会出现失真效果

```
<img width="200" height="160" src="http://img1.niutuku.com/hd/1308/32/32-niutuku.com-252068.jpg"/>
```
<img width="200" height="160" src="http://img1.niutuku.com/hd/1308/32/32-niutuku.com-252068.jpg"/>

#### 图像居中
img不能够自己居中，需要放在其他能够居中的标签中实现这个效果，比如h1标签,p标签. 
经常采用的手段是放在div中居中 

属性可设为left、center、right
```
<div align="center">
<img width="200" height="160" src="http://img1.niutuku.com/hd/1308/32/32-niutuku.com-252068.jpg"/>
</div>
```
<div align="center">
<img width="200" height="160" src="http://img1.niutuku.com/hd/1308/32/32-niutuku.com-252068.jpg"/>
</div>
#### 替换图片中的文字
如果图片不存在，默认会显示一个缺失图片，这是不友好的 
所以可以加上alt属性。 
当图片存在的时候，alt是不会显示的；当图片不存在的时候，alt就会出现。

```
<img width="200" height="160" src="http://img1.niutuku.com/hd/1308/32/32-niutuku.com-2520681.jpg" />
 
<br/>
 
<img width="200" height="160" src="http://img1.niutuku.com/hd/1308/32/32-niutuku.com-252068.jpg" alt="这个是一个图片" />
 
<br/>
<img width="200" height="160" src="http://img1.niutuku.com/hd/1308/32/32-niutuku.com-2520681.jpg" alt="这个是一个图片" />
```
<img width="200" height="160" src="http://img1.niutuku.com/hd/1308/32/32-niutuku.com-2520681.jpg" alt="这个是一个图片" />
### 超链接
a 标签，用来显示超链接
#### 当前页面打开超链接
```
<a href="http://www.12306.cn">12306的超链接</a>
```

<a href="http://www.12306.cn">12306的超链接</a>
#### 新页面打开超链接
target属性

```
<a href="http://www.12306.cn" target="_blank">http://www.12306.cn</a>
```
#### 超链接上提示文字

```
<a href="http://www.12306.cn" title="跳转到www.12306.cn">www.12306.cn</a>
```

<a href="http://www.12306.cn" title="跳转到www.12306.cn">www.12306.cn</a>
#### 设置图片为超链接

```
<a href="http://op.hanhande.com/">
<img width="100" height="80" src="http://img1.niutuku.com/hd/1308/32/32-niutuku.com-252068.jpg"/>
</a>
```

<a href="http://op.hanhande.com/">
<img width="100" height="80" src="http://img1.niutuku.com/hd/1308/32/32-niutuku.com-252068.jpg"/>
</a>
### 表格
#### 行列数据
tr(table row)表示行
td(table data)表示列
```
<table>

<tr>
<td>1</td>
<td>2</td>
</tr>
<tr>
<td>3</td>
<td>4</td>
</tr>

</table>
```

<table>

<tr>
<td>1</td>
<td>2</td>
</tr>
<tr>
<td>3</td>
<td>4</td>
</tr>

</table>

#### 表格带边框

table 的border属性
```
<table border="1">
<tr>
<td>1</td>
<td>2</td>
</tr>
<tr>
<td>3</td>
<td>4</td>
</tr>
</table>
```

#### 设置table宽度 
table 的 width属性
px像素

```
<table border="1" width="100px">
<tr>
<td>1</td>
<td>2</td>
</tr>
<tr>
<td>3</td>
<td>4</td>
</tr>
</table>
```
#### 设置单元格宽度的绝对值
td标签的width属性
1单元格设置宽度，其它行自动继承；
2单元格宽度由table宽度和1单元格宽度决定

```
<table border="1" width="200px">
<tr>
<td width="50px">1</td>
<td>2</td>
</tr>
<tr>
<td>3</td>
<td>4</td>
</tr>
</table>
```
#### 单元格宽度相对值
设置td的属性width为百分数

```
<table border="1" width="200px">
<tr>
<td width="80%">1</td>
<td>2</td>
</tr>
<tr>
<td>3</td>
<td>4</td>
</tr>
</table>
```
#### 单元格水平对齐
设置td的align属性：left、center、right
默认left

```
<table border="1" width="200px">
<tr>
<td width="60%" align="left">1</td>
<td>2</td>
</tr>
<tr>
<td align="right">3</td>
<td>4</td>
</tr>
</table>
```

![这里写图片描述](http://img.blog.csdn.net/20170406163858758?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#### 单元格垂直对齐
设置td属性valign
属性值：top、middle、bottom
```
<table border="1" width="200px">
<tr>
<td width="60%" valign="top">1</td>
<td>
	2	<br/>
	2	<br/>
	2	<br/>
</td>
</tr>

<tr>
<td valign="middle">3</td>
<td align="center">
	4	<br/>
	4	<br/>
	4	<br/>
</td>
</tr>

<tr>
<td valign="bottom">5</td>
<td align="right">
	6	<br/>
	6	<br/>
	6	<br/>
</td>
</tr>
</table>
```
#### 列水平合并
设置td属性colspan

```
<table border="1" width="200px">
<tr>
<td colspan="2">1,2</td>
</tr>

<tr>
<td>3</td>
<td>4</td>
</tr>

<tr>
<td>5</td>
<td>6</td>
</tr>
</table>
```

<table border="1" width="200px">
<tr>
<td colspan="2">1，2</td>
</tr>

<tr>
<td>3</td>
<td>4</td>
</tr>

<tr>
<td>5</td>
<td>6</td>
</tr>
</table>

#### 垂直合并
设置td属性rowspan
```
<table border="1" width="200px">
<tr>
<td rowspan="2">1，3</td>
<td> 2</td>
</tr>

<tr>

<td>4</td>
</tr>

<tr>
<td>5</td>
<td>6</td>
</tr>
</table>
```

<table border="1" width="200px">
<tr>
<td rowspan="2">1，3</td>
<td> 2</td>
</tr>

<tr>

<td>4</td>
</tr>

<tr>
<td>5</td>
<td>6</td>
</tr>
</table>

#### 表格背景色
设置 tr 或者 td 的属性bgcolor
```
<table border="1" width="200px">
<tr>
<td bgcolor="red">1</td>
<td> 2</td>
</tr>

<tr bgcolor="green">
<td>3</td>
<td>4</td>
</tr>

<tr>
<td>5</td>
<td bgcolor="yellow">6</td>
</tr>
</table>
```

<table border="1" width="200px">
<tr>
<td bgcolor="red">1</td>
<td> 2</td>
</tr>

<tr bgcolor="gree">
<td>3</td>
<td>4</td>
</tr>

<tr>
<td>5</td>
<td bgcolor="yellow">6</td>
</tr>
</table>

### 列表
列表分无序列表和有序列表 
分别用 ul 标签和 ol 标签表示
#### 无序列表

```
<ul>
<li>路飞</li>
<li>艾斯</li>
</ul>
```

<ul>
<li>路飞</li>
<li>艾斯</li>
</ul>
#### 有序列表

```
<ol>
<li>赤犬</li>
<li>青雉</li>
<li>黄猿</li>
</ol>
```

<ol>
<li>赤犬</li>
<li>青雉</li>
<li>黄猿</li>
</ol>
### 块 div 、span
div、span 都是块标签，快标签本身没有任何显示效果。
通常是用来结合css进行页面布局

#### 块
本身没有显示效果
```
<div> div块 </div>
<span>span块</span>
```

<div> div块 </div>
<span>span块</span>

#### div块布局
style 外边距样式
margin-left:50px	： 左边距50像素
不使用div，需要对每个图像进行处理
使用div 只需设置div

```
 <img style="margin-left:50px" src="https://www.baidu.com/img/xx.png"/>
  <br/>
 <img style="margin-left:50px" src="https://www.baidu.com/img/xx.png"/>

<div style="margin-left:100px" >
 <img src="https://www.baidu.com/img/xx.png"/>
  <br/>
 <img src="https://www.baidu.com/img/xx.png"/>
</div>
```
![这里写图片描述](http://img.blog.csdn.net/20170406171909845?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#### **div和span的区别**
div是块元素，即自动换行 
常见的块元素还有h1,table,p 
span是内联元素，即不会换行 
常见的内联元素还有img,a,b,strong

```
<div>
 第1个div
</div> 
<div>
 第2个div
</div>
<span>
 第1个span
</span>
<span>
 第2个span
</span>
```
### 字体
font 常用属性 color 颜色、size 大小、face 字体

```
<font color = #0000ff size = 5 face="华文行楷">永远的草帽</font>
<font color = "red" size = "+2" face="黑体">红色大2号字体</font>
<font color = #00ff00 size = "-2">永远的草帽</font>
```

<font color = #0000ff size = 5 face="华文行楷">永远的草帽</font>
<font color = "red" size = "+2" face="黑体">红色大2号字体</font>
<font color = #00ff00 size = "-2">永远的草帽</font>

颜色表
http://blog.csdn.net/lizhongping00/article/details/66475718

### 内联框架标签
iframe 内联框架，可以实现在网页中“插入”网页。

```
<iframe src="https://www.baidu.com/" width="600px" height="400px">
</iframe>
```
### 练习

```
<html>
<body>
	<head>
		<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
	</head>
<h1><strong>英雄技能</strong></h1>
<table border="1">

<tr bgcolor="gree">
<td width="110px">
<strong>技能名</strong>
</td>
<td width="50px">
	<strong>触发</strong>
</td>
<td><strong>技能属性</strong></td>
<td><strong>技能效果</strong></td>
<td><strong>图标</strong></td>
</tr>



<tr >
<td>
<strong>坚韧</strong>
</td>
<td>被动</td>
<td colspan="2">如果盖伦近期没有受到伤害或者被敌方技能命中，那么他会每秒回复若干百分比的最大生命值。小兵的伤害不会中断坚韧效果。</td>
<td>
	<img src="http://ossweb-img.qq.com/images/lol/img/passive/Garen_Passive.png"/>
</td>
</tr>

<tr>
<td><strong>致命打击</strong></td>
<td>Q</td>
<td>
	额外伤害：30/55/80/105/130	<br/>
	移动速度提升的持续时间：1.5/2/2.5/3/3.5
</td>
<td>
盖伦移除身上的所有减速效果，并获得30%移动速度加成，持续1.5/2/2.5/3/3.5秒。<br/>
在接下来的4.5秒内，他的下次普通攻击会造成30/55/80/105/130(+1.4)物理伤害，并沉默目标1.5秒。
</td>
<td>
	<img src="http://ossweb-img.qq.com/images/lol/img/spell/GarenQ.png"/>
</td>
</tr>

<tr>
<td><strong>勇气</strong></td>
<td>W</td>
<td>
	主动效果持续时间：2/3/4/5/6	<br/>
	冷却时间：24/23/22/21/20
</td>
<td>
	被动：击杀一个单位会永久提供护甲和魔法抗性加成，最大值：30。		<br/>
	主动：盖伦获得一个持续2/3/4/5/6秒的防御护盾，减少即将到来的30%伤害。
</td>
<td>
	<img src="http://ossweb-img.qq.com/images/lol/img/spell/GarenW.png"/>
</td>
</tr>

<tr>
<td><strong>审判</strong></td>
<td>E</td>
<td>
	每段命中的基础伤害：14/18/22/26/30	<br/>
	每段命中的总攻击力收益系数：34/35/36/37/38%
</td>
<td>
	盖伦快速地旋舞大剑，持续3秒，在持续期间对周围敌人总共造成物理伤害——14/18/22/26/30加上他总攻击力的34/35/36/37/38%(+)，次(英雄每升3级加1次)。		<br/>
	被4次旋转命中的敌方英雄会损失25%的护甲，持续6秒。
</td>
<td>
	<img src="http://ossweb-img.qq.com/images/lol/img/spell/GarenE.png"/>
</td>
</tr>

<tr>
<td><strong>德玛西亚正义</strong></td>
<td>R</td>
<td>
	伤害：175/350/525	<br/>
	失血伤害：28/33/40% 	<br/>
	冷却时间：120/100/80
</td>
<td>
	被动：最近获得最多击杀数的敌人会成为大反派。盖伦的【审判】和普攻会对大反派造成额外真实伤害，伤害值为大反派1%的最大生命值。		<br/>
	主动：盖伦召唤德玛西亚之力，试图斩杀一名敌方英雄，造成的魔法伤害等于175/350/525加上目标的28/33/40%已损失生命值。对大反派造成真实伤害。
</td>
<td>
	<img src="http://ossweb-img.qq.com/images/lol/img/spell/GarenR.png"/>
</td>
</tr>

</table>
</body>
</html>
```
![这里写图片描述](http://img.blog.csdn.net/20170406191934230?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

