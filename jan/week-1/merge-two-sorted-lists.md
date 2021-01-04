# Merge Two Sorted Lists

 Merge two sorted linked lists and return it as a **sorted** list. The list should be made by splicing together the nodes of the first two lists.



```text
Input: l1 = [1,2,4], l2 = [1,3,4]
Output: [1,1,2,3,4,4]
```

**Example 2:**

```text
Input: l1 = [], l2 = []
Output: []
```

**Example 3:**

```text
Input: l1 = [], l2 = [0]
Output: [0]
```

### 思路:

对于这种头结点不确定的情况， 我们可以用dummy head，之后iterate 2 个list，append小的那个到dummy head 之后。

### code:

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode cur = dummy;
        while(l1 != null && l2 != null) {
            if(l1.val < l2.val) {
                cur.next = l1;
                l1 = l1.next;
                cur = cur.next;
            }else{
                cur.next = l2;
                l2 = l2.next;
                cur = cur.next;
            }
        }
        if(l1 != null) {
            cur.next = l1;
        }
        if(l2 != null) {
            cur.next = l2;
        }
        return dummy.next;
    }
}
```

