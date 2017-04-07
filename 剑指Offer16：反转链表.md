> 输入一个链表，反转链表后，输出链表的所有元素。

## 思路
将原链表头部的节点一个一个拆下接到新链表的头部。
## Java实现

```
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Solution {
    public ListNode ReverseList(ListNode head) {
		if(head == null)
            return null;
        
        ListNode newhead = null;
        
        while(head != null){
            ListNode tmp = head.next;
            head.next = newhead;
            newhead = head;
           	head = tmp;
        }
        return newhead;
    }
}
```