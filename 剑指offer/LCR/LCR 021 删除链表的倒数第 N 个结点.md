给定一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

```
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
```

**示例 2：**

```
输入：head = [1], n = 1
输出：[]
```

**示例 3：**

```
输入：head = [1,2], n = 1
输出：[1]
```

 

**提示：**

- 链表中结点的数目为 `sz`
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`





题目链接：https://leetcode.cn/problems/SLwz0R/





解题步骤如下：

1. 使用双指针，一个指向链表的头结点，另一个指向第 n+1 个结点（从头开始计数）。
2. 移动两个指针，直到第二个指针到达链表的末尾。
3. 删除第一个指针指向的结点，即倒数第 n 个结点。

以下是对应的Java代码：

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0); // 创建一个虚拟头结点，简化边界条件处理
        dummy.next = head;

        ListNode first = dummy;
        ListNode second = dummy;

        // 将第二个指针移动到第 n+1 个结点
        for (int i = 0; i <= n; i++) {
            second = second.next;
        }

        // 同时移动两个指针，直到第二个指针到达链表末尾
        while (second != null) {
            first = first.next;
            second = second.next;
        }

        // 删除第一个指针指向的结点
        first.next = first.next.next;

        return dummy.next; // 返回真实的头结点
    }
}
```

这个算法的时间复杂度是 O(L)，其中 L 是链表的长度。在最坏情况下，需要遍历整个链表。