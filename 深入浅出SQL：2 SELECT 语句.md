
```
SELECT * from my_contacts;
```
### 更好的select -- 使用WHERE子句（为搜索提供条件）

```
SELECT * FROM my_contacts WHERE first_name = 'Anne';
```
<font color=#0000ff size=4 face="黑体">注意，文本字符串要加单引号。</font>

星号（*）表示RDBMS返回表中的所有列。

### 练习：
```
CREATE DATABASE drinks;

USE drinks;

CREATE TABLE easy_drinks(
 drink_name VARCHAR(30),
 main VARCHAR(30),
 amount1 DEC(3,1),
 second VARCHAR(30),
 amount2 DEC(4,2),
 directions VARCHAR(100)
);
```
<font color=#0000ff size=4 face="黑体">注意, amount1 DEC(3,1)中DEC的用法！！</font>

### 查询案例分析

```
SELECT * FROM easy_drinks WHERE main = soda;
会报错，VARCHAR变量需要以单引号引起。

WHERE main = "orange juice";   
正确（双引号）
--但是不要使用双引号，在编程语言中“”表示其中是SQL语句。

WHERE amount2 < '1'; 
可以正常运作，虽然DEC变量不需要引号
```

![这里写图片描述](http://img.blog.csdn.net/20170328221540350?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


### 单引号是特殊字符
插入包含单引号的VARCHAR 、CHAR、BLOB数据时，必须声明数据中的单引号是文本的一部分。加<font color=#0000ff size=4 face="黑体">反斜杠---转义</font>。

```
INSERT INTO my_contacts (location) VALUES('lzp\'s house');
```

#### INSERT包含单引号的数据

1  使用反斜杠转移\

```
'lzp\'s house'
```
2  或者使用另一个单引号

```
'lzp''s house'
```
<font color=#0000ff size=4 face="黑体">WHERE子句也需要转义</font>

```
SELECT * FROM my_contacts WHERE location = 'lzp\'s house';
```
### 比较运算符

= 	是等号
<>	不等号
<		小于  >      大于
<=  >=      

```
SELECT drink_name FROM drink_info WHERE const >= 3.5 AND calories < 50;
```
#### 对文本数据套用比较运算符
<font color=#0000ff size=4 face="黑体">字符表顺序查询</font>

```
SELECT drink_name FROM drink_info WHERE drink_name >= 'L' AND drink_name < 'M';
```
### AND OR
AND 同时满足条件
OR 	满足一个条件即可

```
SELECT drink_name FROM easy_drinks WHERE main = 'cherry juice' OR second = 'cherry juice';
```
<font color=#ff0000 size=4 face="黑体">注意：不要放任表中存在大量的NULL，因为无法直接从表中选择NULL</font>

### NULL
#### 找到值为NULL的分类
```
SELECT drink_name FROM drink_info WHERE calories IS NULL;
```
<font color=#ff0000 size=4 face="黑体">注意：IS NULL 是关键字！！</font>

#### 间接获取NULL
通过不能够满足的条件，选取结果就是NULL。


### LIKE -- 查找部分文本字符串，并返回所有符合条件的行

例：找到所有以CA结尾的值

```
SELECT * FROM my_contacts WHERE location LIKE '%CA';
```
### 通配符
#### % --- 任意数量的未知字符的替身
#### _ --- 一个未知字符的替身

```
SELECT first_name FROM my_contacts WHERE first_name LIKE '_im';
```
### BETWEEN 范围

```
SELECT drink_name FROM drink_info WHERE calories BETWEEN 30 AND 60;
 [30,60]
```
等同于

```
WHERE calories >= 30 AND calories <= 60;
```
<font color=#ff0000 size=4 face="黑体">陷阱</font>

```
WHERE calories BETWEEN 60 AND 30; 中间没有任何值，故查不出结果
小的数在前面
```
### IN -- 满足范围内的任何值，则返回该行或该列

```
SELECT date_name FROM black_book WHERE rating IN {'innovative', 'fabulous');
```
NOT IN **表示不在集合内**。

### NOT
NOT 可以和BETWEEN 或 LIKE 一起使用。
重点在于<font color=#0000ff size=4 face="黑体">NOT 一定要紧接在WHERE （或AND / OR）后面</font>



```
SELECT drink_name FROM drink_info WHERE NOT carbs BETWEEN 3 AND 5;

SELECT date_name from black_book WHERE NOT date_name LIKE 'A%' AND NOT date_name LIKE 'B%';
```

<font color=#0000ff size=4 face="黑体">NOT IN是个例外</font>
但也可以表示为

```
SELECT * FROM easy_drinks WHERE NOT main IN ('soda','iced tea');
```

#### NOT 和 NULL

```
SELECT * FROM easy_drinks WHERE NOT main IS NULL;
或
SELECT * FROM easy_drinks WHERE main IS NOT NULL;
```

