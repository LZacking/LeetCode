定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

​               



**示例:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```

​                 





这个问题可以通过使用辅助栈来实现，辅助栈用于存储当前栈中的最小元素。具体的解题步骤如下：

1. 使用两个栈，一个栈称为`stack`，用于存储正常的栈元素，另一个栈称为`minStack`，用于存储当前栈中的最小元素。

2. 当执行`push`操作时，将元素压入`stack`中，并判断元素是否小于等于`minStack`的栈顶元素（最小元素）。如果是，则也将元素压入`minStack`中，保持`minStack`栈顶元素为当前栈中的最小元素。

3. 当执行`pop`操作时，从`stack`中弹出元素，并且判断弹出的元素是否等于`minStack`的栈顶元素（最小元素）。如果是，则同时从`minStack`中弹出栈顶元素，以保持`minStack`栈顶元素为当前栈中的最小元素。

4. 当执行`top`操作时，直接返回`stack`的栈顶元素。

5. 当执行`min`操作时，直接返回`minStack`的栈顶元素，因为`minStack`中的栈顶元素始终是当前栈中的最小元素。

下面是用Java代码实现上述逻辑的MinStack类：

```java
import java.util.Stack;

class MinStack {
    private Stack<Integer> stack;    // 主栈，存储正常的栈元素
    private Stack<Integer> minStack; // 辅助栈，存储最小元素

    /** initialize your data structure here. */
    public MinStack() {
        stack = new Stack<>();
        minStack = new Stack<>();
    }

    public void push(int x) {
        stack.push(x);
        if (minStack.isEmpty() || x <= minStack.peek()) {
            minStack.push(x);
        }
    }

    public void pop() {
        if (!stack.isEmpty()) {
            int top = stack.pop();
            if (top == minStack.peek()) {
                minStack.pop();
            }
        }
    }

    public int top() {
        if (!stack.isEmpty()) {
            return stack.peek();
        }
        throw new RuntimeException("栈为空");
    }

    public int min() {
        if (!minStack.isEmpty()) {
            return minStack.peek();
        }
        throw new RuntimeException("栈为空");
    }
}
```

这样，我们通过使用辅助栈`minStack`来实现了在O(1)时间复杂度内获取栈的最小元素的要求。