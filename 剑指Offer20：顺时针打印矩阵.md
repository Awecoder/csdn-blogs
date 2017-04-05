> 题目：
>输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.

## **题目分析**
思路：
1 从外到内，一圈一圈依次进行（<font color = #0000ff size = 4> 关键在于找到终止条件</font>）

2 每一圈顺时针打印（<font color = #0000ff size = 4>关键在于每一圈四个角元素的确定和每一步的前提条件</font>）

## **Java实现**

```
import java.util.ArrayList;

public class Solution {
	ArrayList<Integer> list = new ArrayList<>();

	public ArrayList<Integer> printMatrix(int[][] matrix) {
		int rows = matrix.length;
		int cols = matrix[0].length;
		
		if (matrix == null || cols <= 0 || rows <= 0)
			return null;

		int start = 0;

		// 从外到内，一层一层
		while (cols > start * 2 && rows > start * 2) {
			printMatrixInCircle(matrix, cols, rows, start);
			++start;
		}
		return list;
	}

	public void printMatrixInCircle(int[][] array, int cols, int rows, int start) {
		int endCol = cols - 1 - start;
		int endRow = rows - 1 - start;

		// 从左到右打印一行
		for (int i = start; i <= endCol; ++i) { // 第一步总是需要的
			list.add(array[start][i]);
		}

		// 从上到下打印一列
		if (start < endRow) { // 终止行号大于起始行号
			for (int i = start + 1; i <= endRow; ++i) {
				list.add(array[i][endCol]);
			}
		}

		// 从左到右打印一行
		if (start < endCol && start < endRow) { // 需要终止行号大于起始行号，终止列号大于起始列号
			for (int i = endCol - 1; i >= start; --i) {
				list.add(array[endRow][i]);
			}
		}

		// 从下到上打印一行
		if (start < endCol && start < endRow - 1) { // 终止列号大于起始列号（这样才有机会回头），终止行号比起始行号大于等于2
			for (int i = endRow - 1; i >= start + 1; --i) {
				list.add(array[i][start]);
			}
		}
	}
}
```
### 扩展
此题与矩阵旋转有很多类似之处，可相互参考学习
http://blog.csdn.net/lizhongping00/article/details/63738464
