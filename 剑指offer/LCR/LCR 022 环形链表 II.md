给定一个链表，返回链表开始入环的第一个节点。 从链表的头节点开始沿着 `next` 指针进入环的第一个节点为环的入口节点。如果链表无环，则返回 `null`。

为了表示给定链表中的环，我们使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 `pos` 是 `-1`，则在该链表中没有环。**注意，pos 仅仅是用于标识环的情况，并不会作为参数传递到函数中。**

**说明：**不允许修改给定的链表。



 

**示例 1：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist.png)

```
输入：head = [3,2,0,-4], pos = 1
输出：返回索引为 1 的链表节点
解释：链表中有一个环，其尾部连接到第二个节点。
```

**示例 2：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test2.png)

```
输入：head = [1,2], pos = 0
输出：返回索引为 0 的链表节点
解释：链表中有一个环，其尾部连接到第一个节点。
```

**示例 3：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test3.png)

```
输入：head = [1], pos = -1
输出：返回 null
解释：链表中没有环。
```

 

**提示：**

- 链表中节点的数目范围在范围 `[0, 104]` 内
- `-105 <= Node.val <= 105`
- `pos` 的值为 `-1` 或者链表中的一个有效索引





题目链接：https://leetcode.cn/problems/c32eOV/





分析：

这道题目是关于链表中检测环的问题，要求返回环的入口节点。我们可以使用快慢指针的方法来解决这个问题。

解题步骤：

1. 使用两个指针，分别为快指针（fast）和慢指针（slow），初始时都指向链表的头节点（head）。
2. 利用循环，每次循环中，快指针向前移动两步，慢指针向前移动一步。
3. 如果链表中存在环，那么快指针和慢指针一定会在某个时刻相遇。
4. 当快指针和慢指针相遇后，将其中一个指针重新指向链表头节点，另一个指针保持在相遇点。
5. 接着，两个指针同时向前移动一步，它们的相遇点就是环的入口节点。

Java 代码：

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        // 判断链表是否为空或者只有一个节点，无法形成环
        if (head == null || head.next == null) {
            return null;
        }
        
        // 定义快慢指针
        ListNode slow = head;
        ListNode fast = head;
        
        // 判断是否存在环
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            
            // 快慢指针相遇，存在环
            if (slow == fast) {
                // 将一个指针重新指向头节点
                slow = head;
                
                // 两个指针同时向前移动，相遇点即为环的入口节点
                while (slow != fast) {
                    slow = slow.next;
                    fast = fast.next;
                }
                
                return slow; // 返回环的入口节点
            }
        }
        
        return null; // 不存在环
    }
}
```

这个算法的时间复杂度是 O(N)，其中 N 是链表中的节点数。由于只使用了常数级的额外空间，空间复杂度是 O(1)。

