
## **二进制中1的个数**
> 题目：输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。
### **常规解法**
> 思路：首先把n和1做与运算，判断n的最低位是不是1。接着把1左移1位得到2，在判断n的次低位是不是1。

```
public class Solution {
    public int NumberOf1(int n) {
		int count = 0;
        int flag = 1;
        while(flag != 0){
            if((n & flag) != 0)
                count++;
            flag = flag << 1;
        }
        
        return count;
    }
}
```
<font color=#0000ff size=4 face="黑体">
使用(n & flag) != 0，而不是 n & flag != 0 ！！！！</font>

### **更优解**
> 思路：
> 把一个整数减去1，再和原整数做与运算，会把该整数最右边一个1 变成 0。
> 
> 例：
> 1100
> 1100 - 1 =  1011
> 1100 & 1011 = 1000
```
public class Solution {
    public int NumberOf1(int n) {
		int count = 0;
        while(n != 0){
            ++count;
            n = (n - 1) & n;
        }
        
        return count;
    }
}
```

---

## **<font color=#0000ff size=5 face="黑体">Java中的位运算</font>**
<font size=4>
1.  位与（&）：同1为1
2.  位或（|）：有1 为1
3.  位异或（^）：不同为1
4. 带符号右移（>>）：右移n位，正数左侧补0，负数左侧补1。
5.  带符号左移（<<）：
6. 无符号右移（>>>）：右移n位，正数左侧补0，负数左侧补0（变为正数）。
</font>
**<font color=#0000ff size=4 face="黑体">注意：没有无符号左移(<<<)!!!</font>**
