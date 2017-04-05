## **类对象**
### **类对象**
对象之间的区别区别在于，各对象有不同的属性值（名称、血条、移动速度）
类之间的区别他们的区别在于有不同的方法，不同的属性。

类对象，就是用于描述这种类，都有什么属性，什么方法的

### **获取类对象**
获取类对象有3种方式 .class
1 Class.forName

```
String className = "java.util.Date";
Class cl = Class.forName(className);
```

2 Hero.class

```
类.class
```

3 new Hero().getClass()

```
对象.getClass();
```

 <font color = #0000ff size = 4>一个ClassLoader下，一种类，只会有一个类对象存在。通常一个JVM下，只会有一个ClassLoader。</font>
### **获取类对象的时候，会导致类属性被初始化**
 <font color = #0000ff size = 4>无论什么途径获取类对象，都会导致静态属性被初始化，而且只会执行一次。</font>

## **创建对象**

```
//传统的使用new的方式创建对象
Hero h1 =new Hero();
```

```
//使用反射的方式创建对象
String className = "charactor.Hero";
//类对象
Class pClass=Class.forName(className);
//构造器
Constructor c= pClass.getConstructor();
//通过构造器实例化
Hero h2= (Hero) c.newInstance();

或
Hero h2 = (Hero) Class.forNAME(className).newInstance();
```
整理

```
【Java.lang.Class】
Field[] getField()
Methods[] getMethods()
Constructors[] getConstructors()
分别返回类提供的public域，方法和构造器数组，其中包括父类的公有成员。

Field[] getDeclaredFields()
Methods[] getDeclaredMethods()
Constructors[] getDeclaredConstructors()
分别返回类中声明的全部域、方法和构造器，其中包括私有和受保护成员，但不包括父类成员。

【Java.lang.reflect.Field】
【Java.lang.reflect.Method】
【Java.lang.reflect.Constructor】
常用的有
class[] getExceptionTypes()   描述方法抛出的异常
int getModifiers()   获取构造器、方法或域的修饰符的整数值
String getName()  获取构造器、方法或域名的字符串
Class[]  getParameterTypes()  描述参数类型
Class[]  getReturnType()   描述返回类型

【java.lang.reflect.Modifier】
static String toString(int modifiers)  修饰符的字符串表示修饰符一些判断方法。


```
## **查看设置对象域**
1 查看
Field类中 get方法
如果为private，要设置为

```
f.setAccessible(true);
f.set(h,"teemo");

```
2 调用方法

```
Method m = h.getClass().getMethod("setName",String.class);
// setName 是获取类中方法名
// String.class 是参数类型

m.invoke(h, "盖伦");
// 对h对象调用方法m
```

----
## **反射的运用（好处）**
案例展现

1 业务类
两个类，分别有一个各自的业务方法。

```
package reflection;
 
public class Service1 {
 
    public void doService1(){
        System.out.println("业务方法1");
    }
}
```

```
package reflection;
 
public class Service2 {
 
    public void doService2(){
        System.out.println("业务方法2");
    }
}
```

2  <font color = #0000ff size = 4>非反射方式---切换业务，需要修改代码，重新编译运行</font>

```
package reflection;
 
public class Test {
 
    public static void main(String[] args) {
//      new Service1().doService1();
        new Service2().doService2();
    }
}
```
3  <font color = #0000ff size = 4>反射方式---业务切换不需要修改代码，不需要重新编译，只需要修改配置文件，运行即可</font>
---准备配置文件，存放类名称和要调用的方法名，通过反射调用方法
<font color = #0000ff size = 4>这是Spring框架最基本的原理</font>

spring.txt

```
class=reflection.Service1
method=doService1
```

```
package reflection;
 
import java.io.File;
import java.io.FileInputStream;
import java.lang.reflect.Constructor;
import java.lang.reflect.Method;
import java.util.Properties;
 
public class Test {
 
    @SuppressWarnings({ "rawtypes", "unchecked" })
    public static void main(String[] args) throws Exception {
 
        //从spring.txt中获取类名称和方法名称
        File springConfigFile = new File("e:\\project\\j2se\\src\\spring.txt");
        Properties springConfig= new Properties();
        springConfig.load(new FileInputStream(springConfigFile));
        String className = (String) springConfig.get("class");
        String methodName = (String) springConfig.get("method");
         
        //根据类名称创建类对象
        Class clazz = Class.forName(className);
        //根据方面名称，获取方法
        Method m = clazz.getMethod(methodName);
        //获取构造器
        Constructor c = clazz.getConstructor();
        //根据构造器，实例化出对象
        Object service = c.newInstance();
        //调用对象的指定方法
        m.invoke(service);
         
    }
}
```