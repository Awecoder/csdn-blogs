> 输入一个链表，输出该链表中倒数第k个结点
## **题目解析**
### **思路**
思路1：从头遍历获得节点数n，在从头遍历取得第n-k+1个节点
思路2：【只需遍历链表一次】

<font color=#0000ff >使用双指针，第一个指针从链表的头指针开始遍历向前走k-1，第二个指针保持不动，从第k步开始，第二个指针也开始从链表的头指针开始遍历。当第一个指针到达尾节点时，第二个指针到达倒数第k个节点。</font>
### **Java实现**

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
    public ListNode FindKthToTail(ListNode head,int k) {
		if(head == null || k <= 0)
            return null;
        
        ListNode pre =head;
        ListNode post = null;
        
        for(int i = 0; i < k - 1; i++){
            if(pre.next != null)
                pre = pre.next;
            else
                return null;
        }
        
        post = head;
        
        while(pre.next != null){
            pre = pre.next;
            post = post.next;
        }
        return post;
    }
}
```
## **相关题目思路**
> 求链表的中间节点。如果链表的节点总数为奇数，返回中间节点；如果节点总数为偶数，返回中间两个节点的任意一个。

<font color=#0000ff >解决方法：定义两个指针，同时从链表头部出发，一个指针一次走一步，另一个指针一次走两步。走的快的走到链表末尾，慢的正好在链表中间</font>
> 判断一个单向链表是否形成了环形结构。

<font color=#0000ff >解决方法：定义两个指针，同时从链表头部出发，一个指针一次走一步，另一个指针一次走两步。如果快的追上了慢的指针，那么链表是环形链表</font>