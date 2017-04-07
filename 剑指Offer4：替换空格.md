> 请实现一个函数，将一个字符串中的空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

---
## 实现
网络编程中，URL参数中的特殊字符需要转换为服务器可以识别的字符。转换的规则是‘%’后面跟上ASCII码的两位16进制的表示。
空格： %20
 #号 ：%23

```
public class Solution {
	public String replaceSpace(StringBuffer str) {
		int count = 0;
		for (int i = 0; i < str.length(); i++) {
			if (str.charAt(i) == ' ')
				count++;
		}
		int oldLength = str.length();
		int newLength = str.length() + 2 * count;
		str.setLength(newLength);

		for (int i = oldLength - 1; i >= 0; i--) {
			if (' ' == str.charAt(i)) {
				str.setCharAt(newLength - 1, '0');
				str.setCharAt(newLength - 2, '2');
				str.setCharAt(newLength - 3, '%');
				newLength -= 3;
			} else{
                str.setCharAt(newLength - 1, str.charAt(i));
                newLength--;
            }
				
		}
		return str.toString();
	}
}
```
特别留神：每次往后插入时，需要对newLength进行相应的操作！！
此种解法时间复杂度和空间复杂度很好。

## 另解
下面的解法肯定不能是本题的正确考察目的。但可以借以熟悉万能的“\\\s”的使用！！
```

public class Solution {    
public String replaceSpace(StringBuffer str) {
        return str.toString().replaceAll("\\s", "%20");
}
```
## 小结
> 本题特别注意StringBuffer的用法
> 获取长度： length()
> 获取某位置字符： charAt()
> 设置某位置字符：setCharAt()
> 添加：append()
> 删除：delete(4, 10)   [ 4, 10)
> 插入字符串：insert(4, "there")
> 反转：reverse()
> 
> 从后往前是一种很重要的思想，减少移动次数，提高效率。