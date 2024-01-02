给定两个 **非空链表** `l1`和 `l2` 来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储一位数字。将这两数相加会返回一个新的链表。

可以假设除了数字 0 之外，这两个数字都不会以零开头。

 

**示例1：**

![img](https://pic.leetcode-cn.com/1626420025-fZfzMX-image.png)

```
输入：l1 = [7,2,4,3], l2 = [5,6,4]
输出：[7,8,0,7]
```

**示例2：**

```
输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[8,0,7]
```

**示例3：**

```
输入：l1 = [0], l2 = [0]
输出：[0]
```

 

**提示：**

- 链表的长度范围为` [1, 100]`
- `0 <= node.val <= 9`
- 输入数据保证链表代表的数字无前导 0





题目链接：https://leetcode.cn/problems/lMSNwu/





分析：

这道题目是关于两个链表代表的数字相加的问题。由于数字最高位位于链表的开始位置，因此我们可以考虑使用栈来处理。我们可以将两个链表的节点值压入栈中，然后依次出栈进行相加，并构建新的链表。

解题步骤：

1. 将链表 l1 和 l2 的节点值依次压入两个栈中。
2. 初始化进位 carry 为 0。
3. 创建一个新的链表 dummy 作为结果链表的头节点。
4. 依次出栈两个栈的节点值，并将它们与进位相加，得到新的节点值。
5. 将新的节点插入到结果链表的头部，并更新进位。
6. 最终得到的链表即为两数相加的结果。

Java 代码：

```java
import java.util.Stack;

class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Stack<Integer> stack1 = new Stack<>();
        Stack<Integer> stack2 = new Stack<>();

        // 将链表节点值压入栈
        while (l1 != null) {
            stack1.push(l1.val);
            l1 = l1.next;
        }

        while (l2 != null) {
            stack2.push(l2.val);
            l2 = l2.next;
        }

        int carry = 0;
        ListNode dummy = new ListNode(0);
        
        // 依次出栈相加
        while (!stack1.isEmpty() || !stack2.isEmpty() || carry != 0) {
            int sum = carry;
            if (!stack1.isEmpty()) {
                sum += stack1.pop();
            }
            if (!stack2.isEmpty()) {
                sum += stack2.pop();
            }

            // 插入新节点到结果链表的头部
            ListNode newNode = new ListNode(sum % 10);
            newNode.next = dummy.next;
            dummy.next = newNode;

            // 更新进位
            carry = sum / 10;
        }

        return dummy.next;
    }
}
```

这个算法的时间复杂度是 O(max(N, M))，其中 N 和 M 分别是链表 l1 和 l2 的长度。由于使用了栈，空间复杂度也是 O(max(N, M))。

