## **log4j** 
> 使用Log4j来进行日志输出
> 

### **jar包导入** -- log4j-1.2.17.jar
复制jar包到项目的lib 目录下---->右击jar包---->build path---->configure build path---->Libraries ----> 点击Add External JARS.
### **使用log4j**

```
package log4j;

import org.apache.log4j.BasicConfigurator;
import org.apache.log4j.Level;
import org.apache.log4j.Logger;
 
public class TestLog4j {
	// 基于类对象获取日志对象
    static Logger logger = Logger.getLogger(TestLog4j.class);
    public static void main(String[] args) throws InterruptedException {
    	// 进行默认配置
        BasicConfigurator.configure();
        // 设置日志输出级别
        logger.setLevel(Level.DEBUG);
        // 不同级别的日志输出
        logger.trace("跟踪信息");
        logger.debug("调试信息");
        logger.info("输出信息");
        Thread.sleep(1000);  // 用于观察前后日志输出的时间差
        logger.warn("警告信息");
        logger.error("错误信息");
        logger.fatal("致命信息");
 
    }
}
```

输出结果

```
0 [main] DEBUG log4j.TestLog4j  - 调试信息
0 [main] INFO log4j.TestLog4j  - 输出信息
1001 [main] WARN log4j.TestLog4j  - 警告信息
1001 [main] ERROR log4j.TestLog4j  - 错误信息
1001 [main] FATAL log4j.TestLog4j  - 致命信息
```
上面的程序实现：
1 输出log4j.TestLog4j这个类里的日志
2 是在[main]线程里的日志
3 每句日志消耗的毫秒数（最前面的数字）可观察
4 日志级别可观察
5 日志输出级别范围可以控制，只输出高于DEBUG级别的日志，TRACE级别的日志自动不输出。

<font color = #0000ff size = 4>log4j日志记录级别（由低到高）</font>
org.apache.log4j.Level类，但也可以通过Level类的子类自定义级别。
Level | 描述 | 
---|---
ALL | 各级包括自定义级别
TRACE | 指定细粒度比DEBUG更低的信息事件
DEBUG | 指定细粒度信息事件是**最有用**的应用程序调试
INFO  | 指定能够突出在粗粒度级别的应用程序运行情况的信息的消息
WARN | 指定具有潜在危害的情况
ERROR | 错误事件可能仍然允许应用程序继续运行
FATAL | 指定非常严重的错误事件，这可能导致应用程序中止
OFF | 这是**最高等级**，为了关闭日志记录

其中ALL/OFF为特殊等级。

**程序会打印高于或等于所设置级别的日志，设置的日志等级越高，打印出来的日志就越少。**
## **log4j配置**
### **log4j.properties**
在src目录下添加log4j.properties文件

```
log4j.rootLogger=debug, stdout, R
 
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
 
# Pattern to output the caller's file name and line number.
log4j.appender.stdout.layout.ConversionPattern=%5p [%t] (%F:%L) - %m%n
 
log4j.appender.R=org.apache.log4j.RollingFileAppender
log4j.appender.R.File=example.log
 
log4j.appender.R.MaxFileSize=100KB
# Keep one backup file
log4j.appender.R.MaxBackupIndex=5
 
log4j.appender.R.layout=org.apache.log4j.PatternLayout
log4j.appender.R.layout.ConversionPattern=%p %t %c - %m%n
```
### **TestLog4j**

```
package log4j;

import org.apache.log4j.Logger;
import org.apache.log4j.PropertyConfigurator;
 
public class TestLog4j {
	// 基于类对象获取日志对象
    static Logger logger = Logger.getLogger(TestLog4j.class);
    public static void main(String[] args) throws InterruptedException {
    	// 进行属性配置
        PropertyConfigurator.configure("E:/Javalearn/HOW2J/src/log4j.properties");

        // 不同级别的日志输出
        logger.trace("跟踪信息");
        logger.debug("调试信息");
        logger.info("输出信息");
        Thread.sleep(1000);  // 用于观察前后日志输出的时间差
        logger.warn("警告信息");
        logger.error("错误信息");
        logger.fatal("致命信息");
 
    }
}
```
运行结果

```
DEBUG [main] (TestLog4j.java:17) - 调试信息
 INFO [main] (TestLog4j.java:18) - 输出信息
 WARN [main] (TestLog4j.java:20) - 警告信息
ERROR [main] (TestLog4j.java:21) - 错误信息
FATAL [main] (TestLog4j.java:22) - 致命信息
```
1. 输出在控制台，并且格式有所变化，会显示是哪个类的哪一行输出的信息
2. 不仅在控制台有输出，在把日志输出到项目\example.log 这个位置
### **代码解释**
#### **指定配置文件**

```
PropertyConfigurator.configure("e:\\project\\log4j\\src\\log4j.properties");
```
#### **log4j.properties 解释**
设置日志输出的等级为debug,低于debug不输出
设置日志输出到两种地方，分别叫做 stdout和 R

```
log4j.rootLogger=debug, stdout, R
```
第一个地方stdout, 输出到控制台
```
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
```
输出格式是 %5p [%t] (%F:%L) - %m%n

```
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%5p [%t] (%F:%L) - %m%n
```
第二个地方R, 以滚动的方式输出到文件，文件名是example.log,文件最大100k, 最多滚动5个文件

```
log4j.appender.R=org.apache.log4j.RollingFileAppender
log4j.appender.R.File=example.log
log4j.appender.R.MaxFileSize=100KB
log4j.appender.R.MaxBackupIndex=5
```
输出格式是 %p %t %c - %m%n

```
log4j.appender.R.layout=org.apache.log4j.PatternLayout
log4j.appender.R.layout.ConversionPattern=%p %t %c - %m%n
```
### **格式解释**
log4j日志输出格式一览：
%c 输出日志信息所属的类的全名
%d 输出日志时间点的日期或时间，默认格式为ISO8601，也可以在其后指定格式，比如：%d{yyy-MM-dd HH:mm:ss }，输出类似：2002-10-18- 22：10：28
%f 输出日志信息所属的类的类名
%l 输出日志事件的发生位置，即输出日志信息的语句处于它所在的类的第几行
%m 输出代码中指定的信息，如log(message)中的message
%n 输出一个回车换行符，Windows平台为“rn”，Unix平台为“n”
%p 输出优先级，即DEBUG，INFO，WARN，ERROR，FATAL。如果是调用debug()输出的，则为DEBUG，依此类推
%r 输出自应用启动到输出该日志信息所耗费的毫秒数
%t 输出产生该日志事件的线程名

所以：
%5p [%t] (%F:%L) - %m%n 就表示
宽度是5的优先等级 线程名称 (文件名:行号) - 信息 回车换行

## **log4j.xml**

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE log4j:configuration PUBLIC "-//log4j/log4j Configuration//EN" "log4j.dtd">
  
<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
      
    <appender name="STDOUT" class="org.apache.log4j.ConsoleAppender">
       <layout class="org.apache.log4j.PatternLayout"> 
          <param name="ConversionPattern" value="%d %-5p %c.%M:%L - %m%n"/> 
       </layout> 
    </appender>
   
    <!-- specify the logging level for loggers from other libraries -->
    <logger name="com.opensymphony">
        <level value="ERROR" />
    </logger>
  
    <logger name="org.apache">
         <level value="ERROR" />
    </logger>
    <logger name="org.hibernate">
         <level value="ERROR" />
    </logger>
    
   <!-- for all other loggers log only debug and above log messages -->
     <root>
        <priority value="ERROR"/> 
        <appender-ref ref="STDOUT" /> 
     </root> 
      
</log4j:configuration> 
```
输出结果

```
2017-04-04 20:45:22,331 ERROR log4j.TestLog4j.main:19 - 错误信息
2017-04-04 20:45:22,334 FATAL log4j.TestLog4j.main:20 - 致命信息
```
## 参考资料
http://blog.csdn.net/LIZHONGPING00/article/details/69211393
http://www.yiibai.com/log4j/
http://how2j.cn/k/log4j/log4j-tutorial/1081.html?p=4066