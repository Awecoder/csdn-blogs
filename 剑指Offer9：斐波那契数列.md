## **递归和循环**
递归实现方法代码简洁，但性能不如循环。
<font color=#0000ff size=3 face="黑体">优先采用递归 ！</font>
### **递归的缺点**
<font color=#0000ff size=4 face="黑体">缺点1：递归由于是函数调用自身，而函数调用是有时间和空间的消耗的</font>
每一次函数调用，都需要在内存栈中分配空间以保存参数、返回地址以及临时变量，而且往栈压入数据和弹出数据都需要时间。

<font color=#0000ff size=4 face="黑体">缺点2：递归中有可能很多计算是重复的。</font>
递归的本质是把一个问题分解成两个或者多个小问题。如果小问题存在相互重叠的部分，就存在重复计算。

<font color=#0000ff size=4 face="黑体">缺点3：递归可能引发栈溢出。</font>
因为需要每次函数调用在内存栈中分配空间，而每个进程的栈的容量是有限的。当递归调用层数太多时，就会超出栈的容量，导致栈溢出。

## **斐波那契数列**
>题目： 写一个函数，现在要求输入一个整数n，请你输出斐波那契数列的第n项。
![这里写图片描述](http://img.blog.csdn.net/20170328093514508?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### **不好的解法**

```
public class Solution {
    public int Fibonacci(int n) {
		if(n == 0)
            return 0;
        if(n == 1)
            return 1;
        return Fibonacci(n - 1) + Fibonacci(n - 2);
    }
}
```
不好的原因正是递归调用缺点的第2条，求解过程包含大量重复。时间复杂度是n的指数级别。

### **实用的解法**
> 思路：
> 从下往上计算，根据0和1计算出2，通过1和2计算出3.......
> 
> 时间复杂度为n
```
public class Solution {
    public int Fibonacci(int n) {
		int[] result = {0, 1};
        if(n < 2)
            return result[n];
            
        int fbMinusOne = 1;
        int fbMinusTwo = 0;
        int fbN = 0;
        for(int i = 2; i <= n; ++i){
            fbN = fbMinusOne + fbMinusTwo;
            
            fbMinusTwo = fbMinusOne;
            fbMinusOne = fbN;
        }
        return fbN;
    }
}
```
## **扩展题目1**--实质是斐波那契数列
> 题目：一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级台阶总共有多少种跳法。

```
public class Solution {
    public int JumpFloor(int target) {
		int[] result = {0, 1, 2};
        if(target <= 2)
            return result[target];
        int minusOne = 2;
        int minusTwo = 1;
        int jf = 0;
        for(int i = 3; i <= target; ++i){
            jf = minusOne + minusTwo;
            
            minusTwo = minusOne;
            minusOne = jf;
        }
        return jf;
    }
}
```
## **扩展题目2**
> 一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

```
public class Solution {
    public int JumpFloorII(int target) {
        if(target <= 0)
            return 0;
        return 1 << (target - 1);
    }
}
```
## **扩展题目3**
> 我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？
```
public class Solution {
    public int RectCover(int target) {
        if(target <= 0)
            return 0;
		int[] result = {1, 2};
        if(target <= 2)
            return result[target - 1];
        int one = 2;
        int two = 1;
        int total = 0;
        for(int i = 3; i <= target; i++){
            total = one + two;
            
            two = one;
            one = total;
        }
        return total;
    }
}
```