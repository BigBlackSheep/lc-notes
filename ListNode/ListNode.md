
https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/
#####19. 删除链表的倒数第N个节点
这道题使用快慢指针 删除倒数第n个节点
先使用for loop 把快指针移动到距离慢指针n+1的位置上
之后使用 while loop 遍历如果快指针=null 则代表已经到头了
而慢指针需要删除next指针了。
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode fast = dummy;
        ListNode slow = dummy;

        for (int i = 0; i < n; i++) {
            fast = fast.next;
        }
        while (fast !=null){
           slow = slow.next;
           fast =fast.next;
        }
        slow.next = slow.next.next;
        return dummy.next;
    }

}
```
https://leetcode-cn.com/problems/intersection-of-two-linked-lists/
#####160. 相交链表
这道题比较有意思
第一步先去遍历A和B两个链表 
如果A已经跑完了,B还没有跑完.则把A放到B起点重新跑,等B跑了把他放到A的起点重新跑
这样做的作用就是 把A和B放到同一个起跑线上.这样才可以判断相交点的值是否一致.
其实就是很简单的原理 **a+b+c =c+b+a**
如果跑完了之后还是没有相交点则退出循环 因为h1 !=h2 最后两个都是Null则退出.
任意返回h1 或 h2均可

```java
class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode h1 =headA;
        ListNode h2 = headB;

        while (h1 != h2 ){
            h1 = h1.next == null ? headB : h1.next;
            h2 = h2.next == null ? headA : h2.next;
        }
        return h1;
    }

}
```


https://leetcode-cn.com/problems/reverse-linked-list/
#####206. 翻转链表
**比较绕不太好理解**
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode curr = head;

        ListNode pre = null;

        while (curr != null){
            //暂存当前节点的下一个
            ListNode temp = curr.next;
            //把当前节点的下一个 指向pre
            curr.next = pre;
            // pre  等于当前期节点
            pre = curr;
            //当前节点等于第一次进来暂存的自己的下一个 等于自己和自己做了一次交换
            curr = temp;
        }
        return pre;
    }

}
```
https://leetcode-cn.com/problems/merge-two-sorted-lists/
#####21. 合并两个有序链表
```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;

        while (l1 !=null && l2!=null){
            if(l1.val > l2.val){
                curr.next = l1;
                l1 = l1.next;
            }else {
                curr.next = l2;
                l2 = l2.next;
            }
            curr = curr.next;
        }
        curr.next = l1 == null ? l2 : l1;
        return dummy.next;
    }
}
```
https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/
#####83. 删除排序链表中的重复元素
```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode curr = head;
        while (curr !=null){
            if(curr.val == curr.next.val){
                curr.next = head.next.next;
            }else {
                curr = curr.next;
            }
        }
        return head;
    }
}
```

https://leetcode-cn.com/problems/swap-nodes-in-pairs/
#####24. 两两交换链表中的节点

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode curr = dummy;

        while (curr.next != null && curr.next.next != null) {
            ListNode next1 = curr.next;
            ListNode next2 = curr.next.next;

            next1.next = next2.next;
            next2.next = next1;

            curr.next = next2;
            curr = curr.next.next;
        }
        return dummy.next;
    }
}
```

