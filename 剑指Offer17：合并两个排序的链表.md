> 题目：输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

## Java实现
### 递归实现

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
    public ListNode Merge(ListNode list1,ListNode list2) {

        if(list1 == null)
            return list2;
        if(list2 == null)
            return list1;
        
        ListNode newList = null;
        
        if(list1.val <= list2.val){
            newList = list1;
            newList.next = Merge(newList.next, list2);
        } else{
            newList = list2;
            newList.next = Merge(list1, newList.next);
        }
      
        return newList;
        
    }
}
```