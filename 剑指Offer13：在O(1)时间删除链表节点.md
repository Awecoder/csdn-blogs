> 题目：给定单向链表的头指针和一个节点指针，定义一个函数在0(1)时间删除该节点。
## **题目分析**
单向链表中删除一个节点，**常规做法**是从链表的头结点开始，顺序变量查找要删除的节点，并在链表中删除该节点。

<font color = #0000ff size = 4>更好的解法：</font>节点i ---> 节点j
**将节点j的内容复制给节点 i，将节点 i 的指针指向节点j的下一个指针。**

此处的其它问题：
1. 删除的节点是头节点，且只有一个节点
2. 删除的节点是尾节点

之前总结的单链表的实现：http://blog.csdn.net/lizhongping00/article/details/63251448

## **Java实现**
```
public class Solution {
	private class ListNode {
		int value;
		ListNode next;
	}

	public static void deleteNode(ListNode first, ListNode toBeDeleted) {
		if (first == null || toBeDeleted == null)
			return;
		// 如果节点是头结点,且只有一个节点
		if (toBeDeleted == first && first.next == null) {
			first = null;
		} else if (toBeDeleted.next != null) { // 要删除节点不是尾节点
			toBeDeleted.value = toBeDeleted.next.value;
			toBeDeleted.next = toBeDeleted.next.next;
		} else { // 链表中有多个节点，删除尾节点，需从头遍历
			ListNode current = first;
			// 找到该节点的前一个节点
			while (current.next != toBeDeleted) {
				current = current.next;
			}
			// 删除该节点
			current.next = null;

		}
	}
}
```
运行结果

```
1->2->3->4->5->6->7->8->9->null
2->3->4->5->6->7->8->9->null
2->3->4->5->6->7->8->null
2->3->4->6->7->8->null
```

**<font color = #ff0000 size = 4>注意，本题需要确认要删除的节点是否包含在链表内。如果未知，仍然需要0(n)来判断是否包含该节点。</font>**