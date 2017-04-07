## **树**
  除了根节点外每个节点只有一个父结点，父结点没有根结点；除了叶子结点外每个节点都有一个或多个子节点，叶子节点没有子结点。父结点和子结点之间用指针链接。

### **树的遍历**

- 前序遍历：根左右（类似图的深度优先遍历）
- 中序遍历：左根右
- 后序遍历：左右根
- 层序遍历：从上往下一层一层（类似图的宽度优先遍历）

### **二叉树** 
1. <font color=#0099ff size=3 face="黑体">左子结点总是小于根结点，右子结点总是大于根结点</font>。查找O(log n）

2. AVL平衡二叉树：相邻的两个子树的高度相差不能大于1.否则进行旋转（左儿子的左子树和右儿子的右子树进行单旋转，左儿子的右子树和右儿子的左子树进行双旋转）。
3.  二叉树的特例: （1）堆分为最大堆和最小堆。最大堆根节点最大，最小堆根节点最小。能快速查找最大最小值。（2）红黑树

## **题目**
> 题目：输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果都不含重复数字。
> 例如，输入前序变量序列{1，2，4，7，3，5，6，8}和中序遍历{4，7，2，1，5，3，8，6}，则重建二叉树并返回。

### **思路**
1. 首先根据前序遍历序列的第一个数字创建根节点，
2. 中序遍历序列中找到根节点的位置，分别确定出根节点左、右子树的序列进行递归。

图解
![这里写图片描述](http://img.blog.csdn.net/20170326214006165?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
### **Java实现**
```
class TreeNode {
	int val;
	TreeNode left;
	TreeNode right;

	TreeNode(int x) {
		val = x;
	}
}

public class Solution {

	public TreeNode reConstructBinaryTree(int[] pre, int[] in) {
		TreeNode root = reConstructBinaryTree(pre, 0, pre.length - 1, in, 0, in.length - 1);
		return root;
	}

	private TreeNode reConstructBinaryTree(int[] pre, int startPre, int endPre, int[] in, int startIn, int endIn) {
		if (startPre > endPre && startIn > endIn)
			return null;
		TreeNode root = new TreeNode(pre[startPre]);

		for (int i = startIn; i <= endIn; i++)
			if (in[i] == pre[startPre]) {
				root.left = reConstructBinaryTree(pre, startPre + 1, startPre + i - startIn, in, startIn, i - 1);
				root.right = reConstructBinaryTree(pre, startPre + i - startIn + 1, endPre, in, i + 1, endIn);
			}
		return root;
	}
}
```
## 小结

<font color=#0000ff size=5 face="黑体">特别注意二叉树中递归的使用！！！ </font>