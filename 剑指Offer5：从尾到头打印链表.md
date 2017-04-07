> 题目： 输入一个链表的头结点，从尾到头反过来打印每个节点的值。
## 栈实现
单链表只能从前往后迭代，从后往前打印，明显就是后进先出（LIFO）——栈。首先通过栈来解决
```
import java.util.ArrayList;
import java.util.Stack;
public class Solution {
ArrayList<Integer> arrayList = new ArrayList<>();
 public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
		Stack<Integer> stack = new Stack<>();
		while(listNode != null){
			stack.push(listNode.val);
			listNode = listNode.next;
		}
		while(!stack.isEmpty()){  // 
			arrayList.add(stack.pop());
		}
		
		return arrayList;
	}
}
```
注意：
1. **栈空使用 isEmpty（）**，而不要使用stack == null。
2. 注意循环的使用

## 递归实现
递归本质是一种栈结构。要实现反过来输出链表，我们每访问一个节点，先递归输出它后面的节点，在输出该节点自身，这样链表的输出结果就反过来了。
```
import java.util.ArrayList;
public class Solution {
    ArrayList<Integer> arrayList = new ArrayList<>();
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        if(listNode != null){
			printListFromTailToHead(listNode.next);
			arrayList.add(listNode.val);
		}
        return arrayList;
        
    }
}
```
注意：
1. 递归终止条件的设定

## 显式用栈代码鲁棒性好于递归（深层递归可能导致栈溢出）