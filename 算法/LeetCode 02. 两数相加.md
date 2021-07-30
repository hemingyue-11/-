# LeetCode 02. 两数相加

![题目](images\leetcode02.png)

## 思路一：

首先想到的是先把链表转化为数字，然后数字相加后转为链表，但是由于链表太长导致超出了容量。错误（：

## 思路二：

虽然链表表示的形式时逆序，但是仍然可以考虑运用加减法的流程。两个链表左端对齐，两个链表的对应位以及进位（0或1）相加，大于九就向前进一位，直到两个链表的当前节点都为null。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode head = new ListNode(0); //当作哨兵，返回哨兵的下一个节点
        ListNode cur = head;
        int flag = 0; //用来表示进位
        int sum = 0; //表示当前位的和
        while (l1 != null || l2 != null) {
            if (l1 == null) {
                sum = l2.val + flag;
            } else if (l2 == null) {
                sum = l1.val + flag;
            } else {
                sum = l1.val + l2.val + flag;
            }
            if ( sum > 9 ) {
                flag = 1;
                cur.next = new ListNode(sum % 10);
            } else {
                flag = 0;
                cur.next = new ListNode(sum);
            }
            cur = cur.next;
            if (l1 != null) l1 = l1.next;
            if (l2 != null) l2 = l2.next;
        }
        //循环结束后进位可能为1
        if (flag == 1) {
            cur.next = new ListNode(1);
        }
        return head.next;
    }
}
```

