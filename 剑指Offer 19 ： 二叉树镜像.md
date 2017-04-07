> 题目：请完成一个函数，输入一个二叉树，该函数输出它的镜像。

## 题目分析
思路：
1. 根节点判空
2. 交换根节点左右两个子节点的位置
3. 如果左右两个子节点不为空，分别交换其左右子树。
4. 遍历到叶子之后，便得到了镜像。

## Java实现
### 递归实现

```
public class TreeNode {
    int val = 0;
    TreeNode left = null;
    TreeNode right = null;

    public TreeNode(int val) {
        this.val = val;

    }

}
*/
public class Solution {
    public void Mirror(TreeNode root) {
        // 当前节点不为空操作
        if(root == null)
            return ;
        if(root.left == null && root.right == null)
            return ;
        
        // 交换左右两个子节点的位置
        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;
        
        // 递归实现左右子节点的镜像
        if(root.left != null)
            Mirror(root.left);
        if(root.right != null)
            Mirror(root.right);
    }
}
```