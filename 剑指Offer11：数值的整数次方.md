> 题目：给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

## Java实现
```
package offer;
/*
 * 高效的幂运算
 */
public class Solution {
	public static double Power(double base, int exponent) {
		int exp = Math.abs(exponent);  // 将指数转换为正数
		
		if (exp == 0)
			return 1;
		if (exp == 1)
			return base;

		// exp 15 7 3 1 
		// exp 14 7 3 1 
		double result = Power(base, exp >> 1);  
		result *= result;
		if ((exp & 0x1) == 1)  // 如果为奇数，乘以 base
			result *= base;
		if(exponent < 0)
			result = 1 / result;

		return result;
	}
	public static void main(String[] args) {
		System.out.println(Power(4,-2));
	}
}
```
## 小结
本身采用这种递归平方就非常的高效，同时使用右移运算符>>和位与运算符 & 进行优化。
两处细节：
base是否等于0：本题中base为0，且为分母时，返回Infinity（无穷）
位运算代替乘除法以及求余运算。

稍差一点的代码

```
public static long pow(long x, int n){
	if(n == 0)
		return 1;
	if(n == 1)
		return x;
	
	if(n % 2 == 0)
		return pow(x * x, n / 2);
	else
		return pow(x * x, n / 2) * x;
}
```