> 题目：
> 输入数字n，按顺序打印出从1 最大的 n位十进制数。比如输入3，打印 1、2、3 一直到最大的3 位数即999。

## **题目分析**
本题没有规定n的范围，故int、long都可能会溢出，是典型的<font color = #0000ff size = 4>大数问题</font>。（<font color = #ff0000 size = 5>本题1号坑</font>）

<font color = #0000ff size = 4>大数问题的解决方法</font>
使用字符串或者字符数组表达大数。
字符数组中每个字符都是'0'-'9' 中的某个字符。

### **第一部分**
首先把字符数组中的每个数字都初始化为'0'，然后每一次为字符串表示的数字加1，再打印出来。我们需要做两件事：
1.  在字符数组表达的数字上模拟加法
2.  把字符数组表达的数字打印出来

```
	public static void print1ToMaxOfN(int n) {
		if (n <= 0)
			return;
		// 初始化一个全为'0'的字符数组
		char[] number = new char[n];
		for (int i = 0; i < n; i++) {
			number[i] = '0';
		}
		// 判断是否最大，如果没有打印数字
		while (!increment(number)) {
			printNumber(number);
		}
	}
```
increment 表示模拟数字加 1，并判断是否在最左侧位是否大于等于10，等于10返回溢出。
printNumber 打印数字
### **第二部分：模拟数字加 1，并判断是否到达最大值。**


<font color = #0000ff size = 4>判断是否已经到达最大值</font>：（<font color = #ff0000 size = 5>本题2号坑</font>）
每个数与最大数比较不可取，时间复杂度为O(n）. <font color = #00ff00 size = 4>不可取</font>

在字符数组第一个字符进位，第一个字符加1产生进位的时候，就说明已经是最大值。 
9999-->10000   复杂度O(1)

```
	private static boolean increment(char[] number) {
		boolean isOverflow = false;   // 是否溢出
		int nTakeOver = 0;            // 进位标志
		int nLength = number.length;  // 字符数组长度

		for (int i = nLength - 1; i >= 0; i--) {  // 4 3 2 1 0
			int nSum = number[i] - '0' + nTakeOver; 
			if(i == nLength - 1)      // 在第n-1个字符模拟加 1
				nSum++;
			
			if(nSum >= 10){    // 数组某位置的值=10，需要进位了
				if(i == 0){    // 如果是第 1 个字符，溢出标志变为true
					isOverflow = true;
				} else {       // 该位置值-10，进位标志=1，等下一次循环（i-1）时，+1
					nSum -= 10;
					nTakeOver = 1;
					number[i] = (char) ('0' + nSum);  // 更新该位置值
				}
			}
			else{              // 如果没到进位，正常更新该下标位置值
				number[i] = (char) ('0' + nSum);
				break;
			}
		}
		return isOverflow;
	}
```
### **第三部分：打印字符**
打印字符，用于补位的0是不应该打印出来的（<font color = #ff0000 size = 5>本题3号坑</font>）
```
	private static void printNumber(char[] number) {
		boolean isBeginning0 = true;  // 字符为0标志
		int nLength = number.length;
		
		for(int i = 0; i < nLength; ++i){
			if(isBeginning0 && number[i] !='0'){
				isBeginning0 = false;
			}
			if(!isBeginning0){
				System.out.printf("%c",number[i]);	
			}
		}
		System.out.println();
	}
```
## **Java实现**

```
package offer;

/*
 * 高效的幂运算
 */
public class Solution {
	public static void print1ToMaxOfN(int n) {
		if (n <= 0)
			return;
		// 初始化一个全为'0'的字符数组
		char[] number = new char[n];
		for (int i = 0; i < n; i++) {
			number[i] = '0';
		}
		// 判断是否最大，如果没有打印数字
		while (!increment(number)) {
			printNumber(number);
		}
	}

	private static void printNumber(char[] number) {
		boolean isBeginning0 = true; // 字符为0标志
		int nLength = number.length;

		for (int i = 0; i < nLength; ++i) {
			if (isBeginning0 && number[i] != '0') {
				isBeginning0 = false;
			}
			if (!isBeginning0) {
				System.out.printf("%c", number[i]);
			}
		}
		System.out.println();
	}

	private static boolean increment(char[] number) {
		boolean isOverflow = false; // 是否溢出
		int nTakeOver = 0; // 进位标志
		int nLength = number.length; // 字符数组长度

		for (int i = nLength - 1; i >= 0; i--) { // 4 3 2 1 0
			int nSum = number[i] - '0' + nTakeOver;
			if (i == nLength - 1) // 在第n-1个字符模拟加 1
				nSum++;

			if (nSum >= 10) { // 数组某位置的值=10，需要进位了
				if (i == 0) { // 如果是第 1 个字符，溢出标志变为true
					isOverflow = true;
				} else { // 该位置值-10，进位标志=1，等下一次循环（i-1）时，+1
					nSum -= 10;
					nTakeOver = 1;
					number[i] = (char) ('0' + nSum); // 更新该位置值
				}
			} else { // 如果没到进位，正常更新该下标位置值
				number[i] = (char) ('0' + nSum);
				break;
			}
		}
		return isOverflow;
	}

	public static void main(String[] args) {
		print1ToMaxOfN(2);
	}
}
```
## **递归解法（TODO）**

## **小结：特别注意大数问题！！**
关于n位的整数，并且没有限定 n 的取值范围，或者是输入任意大小的整数！！！
考虑使用字符串或字符数组解决！！