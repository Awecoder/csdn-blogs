> 输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则输出True,否则输出False。假设输入的数组的任意两个数字都互不相同。
## 题目分析
思想：
后序遍历的顺序是左右根。
后序遍历序列的最后一个数字是数根节点的值。
序列数字分为两部分：一部分是左子树节点的值，比根节点的值小；另一部分是右子树节点的值，比根节点的值大。
## Java实现
```
public class Solution {
	public boolean VerifySquenceOfBST(int[] sequence) {
		// 判空
		if (sequence == null | sequence.length <= 0)
			return false;

		return this.isBST(sequence, 0, sequence.length - 1);
	}

	private boolean isBST(int[] sequence, int lo, int hi) {
		// 如果对应要处理的数据只有一个或者已经没有数据要处理（start>end）就返回true
		if (lo >= hi)
			return true;

		// 在二叉树中左子树的节点小于根节点 [lo, i)
		// 找到一个不大于根节点的位置
		int i = lo;
		for (; i < hi; i++) {    // hi 位置是root的值
			if (sequence[i] > sequence[hi])
				break;
		}

		// 在二叉树中右子树的节点大于根节点 [i, hi)
		// 如果右子树节点小于根节点，说明不是二叉查找树
		int j = i;
		for (; j < hi; j++) {
			if (sequence[j] < sequence[hi])
				return false;
		}

		// 判断左子树是否是二叉查找树
		boolean left = true;
		if (i > 0) {
			left = isBST(sequence, lo, i - 1); // 此时 i - 1 是左子树的根节点
		}
		// 判断右子树是否是二叉查找树
		boolean right = true;
		if (i < hi)
			right = isBST(sequence, i, hi - 1); // 此时 hi - 1 是右子树的根节点
		return left && right;
	}
}
```