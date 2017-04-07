> 题目：输入两棵二叉树A 和 B，判断B是不是A的子结构。
## 思路
第一步：首先在树A 中遍历与根结点值一样的结点R。
第二步：找到值相同的结点后，判断树A中以R为根结点的子树是否包含树B一样的结构。
## Java实现
```
class TreeNode {
	int val = 0;
	TreeNode left = null;
	TreeNode right = null;
}

public class Solution {
	public boolean HasSubtree(TreeNode root1, TreeNode root2) {
		boolean result = false;

		if (root1 != null && root2 != null) {
			if (root1.val == root2.val)
				result = doesTree1HaveTree2(root1, root2);

			// 如果不匹配就找树A的左子结点和右子结点进行判断
			if (!result)
				result = HasSubtree(root1.left, root2);
			if (!result)
				result = HasSubtree(root1.right, root2);
		}

		return result;
	}

	public static boolean doesTree1HaveTree2(TreeNode root1, TreeNode root2) {
		if (root2 == null)  // 特别注意此处的终止条件
			return true;
		if (root1 == null)
			return false;

		if (root1.val != root2.val)
			return false;

		return doesTree1HaveTree2(root1.left, root2.left) && doesTree1HaveTree2(root1.right, root2.right);
	}
}
```