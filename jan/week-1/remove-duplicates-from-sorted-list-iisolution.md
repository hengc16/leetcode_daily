# Remove Duplicates from Sorted List IISolution

 Given the `head` of a sorted linked list, _delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list_. Return _the linked list **sorted** as well._

\_\_

**Example 1:**![](https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg)

```text
Input: head = [1,2,3,3,4,4,5]
Output: [1,2,5]
```

**Example 2:**![](https://assets.leetcode.com/uploads/2021/01/04/linkedlist2.jpg)

```text
Input: head = [1,1,1,2,3]
Output: [2,3]
```

### 思路:

因为头结点不定，可以用dummy head。 设2个指针，pre 和 cur。 dummy.next 到 pre的为最终结果。 cur为iterate 指针。 

如果  cur 和cur next 相同， 说明都不可取， 则一直跳过到 cur 和 cur 不同， 这时让pre的next指向cur的next。

### Code:

```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode dummy = new ListNode(0);
        ListNode pre = dummy;
        dummy.next = head;
        ListNode cur = head;
        while(cur != null) {
            //skip all the dup
            if(cur.next != null && cur.val == cur.next.val){
                while(cur.next != null && cur.val == cur.next.val) {
                cur = cur.next;
                }
                pre.next = cur.next;
            }
            else{
                pre = pre.next;
            }
            cur = cur.next;
        }
        return dummy.next;
    }
}
```





