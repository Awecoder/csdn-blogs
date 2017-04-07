> 题目：在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
> 1  2  8  9
> 2 4  9 12
> 4 7 10 13
> 6 8 11 15

---
## 解法一
> 分析：
> 如果我们从左上角开始查找便会发现，比较过后数字会出现在下方和右方，不易运算。故，
> 首先，选取**数组中右上角的数字**（突破口）。
> 如果该数字等于要查找的数字，查找结束；
> 如果该数字大于要查找的数字，剔除数字所在列（在该列左侧查找col--）；
> 如果该数字小于要查找的数字，则剔除所在的行（row++，已经列最大了）。
> 循环查找。

```
public class Solution {
	public boolean Find(int target, int[][] array) {

		if (array == null)
			return false;
		int row = 0;
		int col = array[0].length - 1;
		while (row < array.length && col >= 0) {
			if (target == array[row][col])
				return true;
			else if(target > array[row][col])
				row++;
			else
				col--;
		}
		return false;
	}
}
```
## 解法二：二分查找

```
public class Solution {
	public boolean Find(int target, int[][] array) {
		if (array == null)
			return false;
		for (int i = 0; i < array.length; i++) {
			int lo = 0;
			int hi = array[0].length - 1;
			while (lo <= hi) {
				int mid = (lo + hi) / 2;
				if (array[i][mid] > target)
					hi = mid - 1;
				else if (array[i][mid] < target)
					lo = mid + 1;
				else
					return true;
			}
		}
		return false;
	}
}
```
## 注意

> 二维数组：
> 行 row ： arr.length
> 列 col  ： arr[0].length

认真分析两种解法！！