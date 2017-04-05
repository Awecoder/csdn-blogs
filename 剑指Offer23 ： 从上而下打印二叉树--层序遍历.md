> 题目：从上往下打印出二叉树的每个节点，同层节点从左至右打印。
## 题目分析
本题实质是广度优先遍历二叉树。层序打印节点。
思想：打印父节点，将孩子放入队列中。
具体规律：
不管是广度优先遍历一个有向图，还是一棵树，都要用到队列。第一步我们把起始结点（对树而言是根结点）放入到队列中。接下来每一次从队列的头部取出一个结点，遍历这个结点之后把它从它能到达的结点（对树而言是子结点）都依次放入队列中。重复这个比那里过程，直到队列中的结点全部被遍历为止。
## Java实现

```
package offer;

import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;

public class Solution {
	class TreeNode {
		int val = 0;
		TreeNode left = null;
		TreeNode right = null;

		public TreeNode(int val) {
			this.val = val;

		}

	}

	public ArrayList<Integer> PrintFromTopToBottom(TreeNode root) {
		ArrayList<Integer> list = new ArrayList<>();
		Queue<TreeNode> queue = new LinkedList<>();
		if (root == null)
			return list;

		TreeNode node = null;

		queue.add(root); // 添加根节点

		// 终止条件：队列为空
		while (!queue.isEmpty()) {
			// 弹出父节点
			node = queue.poll();
			
			// 父节点的孩子入队
			if (node.left != null)
				queue.add(node.left);
			if (node.right != null)
				queue.add(node.right);
			list.add(node.val);
		}
		return list;
	}
}
```