## **Log4j**
log4j是一个用Java编写的可靠，快速和灵活的日志框架（API），它在Apache软件许可下发布。 

Log4j是高度可配置的，并可通过在运行时的外部文件配置。它根据记录的优先级别，并提供机制，以指示记录信息到许多的目的地，诸如：数据库，文件，控制台，UNIX系统日志等。
Log4j中有三个主要组成部分：

**loggers**: 负责捕获记录信息。

**appenders** : 负责发布日志信息，以不同的首选目的地。

**layouts**: 负责格式化不同风格的日志信息。
## **log4j安装配置**
如果在Window上开发使用Eclipse的话，可以在Eclipse创建用户库并加入到构建路径中。
## **log4j架构**
Log4j API设计为分层结构，其中每一层提供了不同的对象，对象执行不同的任务。这使得设计灵活，根据将来需要来扩展。

有两种类型可用在Log4j的框架对象。
**核心对象**： 框架的强制对象和框架的使用。
**支持对象**： 框架和支持体核心对象，可选的对象执行另外重要的任务。
### **核心对象**
#### **Logger对象：**

顶级层的Logger，它提供Logger对象。Logger对象<font color = #0000ff size = 4>负责捕获日志信息及它们存储在一个空间的层次结构。</font>
####**布局对象：**

该层提供其<font color = #0000ff size = 4>用于格式化不同风格的日志信息的对象</font>。布局层提供支持Appender对象到发布日志信息之前。

布局对象的发布方式是人类可读的及可重复使用的记录信息的一个重要的角色。

#### **Appender对象：**

下位层提供Appender对象。Appender对象<font color = #0000ff size = 4>负责发布日志信息</font>，以不同的首选目的地，如数据库，文件，控制台，UNIX系统日志等。

以下是显示Log4J框架的不同组件的虚拟图：
![这里写图片描述](http://img.blog.csdn.net/20170404212436111?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
### **支持对象**
log4j框架的其他重要的对象起到日志框架的一个重要作用：

####**Level对象：**

级别对象定义的任何记录信息的**粒度和优先级**。有记录的七个级别在API中定义：OFF, DEBUG, INFO, ERROR, WARN, FATAL 和 ALL

####**Filter对象：**

过滤对象用于**分析日志信息**及是否应记录或不用这些信息做出进一步的决定。

一个appender对象可以有与之关联的几个Filter对象。如果日志记录信息传递给特定Appender对象，都和特定Appender相关的Filter对象批准的日志信息，然后才能发布到所连接的目的地。

####**对象渲染器：**

ObjectRenderer对象是一个指定提供传递到日志框架的不同对象的**字符串表示**。这个对象所使用的布局对象来准备最后的日志信息。

####**日志管理：**

日志管理对象管理的**日志框架**。它负责从一个系统级的配置文件或配置类读取初始配置参数。
## log4j配置
### log4j.properties 语法


log4j.properties 文件的一个appender X的语法
```
# Define the root logger with appender file
log4j.rootLogger = DEBUG, FILE

# Define the file appender
log4j.appender.FILE=org.apache.log4j.FileAppender
log4j.appender.FILE.File=${log}/log.out

# Define the layout for file appender
log4j.appender.FILE.layout=org.apache.log4j.PatternLayout
log4j.appender.FILE.layout.conversionPattern=%m%n
```
1 根日志记录器(logger)的级别定义为DEBUG并连接附加器命名为FILE
2 附加器(appender)File是定义为org.apache.log4j.FileAppender并写入到一个名为“log.out”位于日志log目录下

3 定义的布局模式是%m%n，这意味着每打印日志消息之后，将加上一个换行符

参考资料
http://blog.csdn.net/lizhongping00/article/details/69211410
http://www.yiibai.com/log4j/
http://how2j.cn/k/log4j/log4j-tutorial/1081.html?p=4066