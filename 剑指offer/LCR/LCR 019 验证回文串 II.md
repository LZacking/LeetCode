给定一个非空字符串 `s`，请判断如果 **最多** 从字符串中删除一个字符能否得到一个回文字符串。

 

**示例 1:**

```
输入: s = "aba"
输出: true
```

**示例 2:**

```
输入: s = "abca"
输出: true
解释: 可以删除 "c" 字符 或者 "b" 字符
```

**示例 3:**

```
输入: s = "abc"
输出: false
```

 

**提示:**

- `1 <= s.length <= 105`
- `s` 由小写英文字母组成





题目链接：https://leetcode.cn/problems/RQku0D/





解题步骤如下：

1. 使用双指针，一个指向字符串的开头，另一个指向字符串的末尾。
2. 检查两个指针指向的字符是否相同，如果相同，则继续向中间移动。
3. 如果遇到不同的字符，尝试删除其中一个字符，然后分别判断删除一个字符后的两个子串是否是回文串。
4. 如果删除一个字符后的任意一个子串是回文串，则返回 true；否则，返回 false。

以下是对应的Java代码：

```java
class Solution {
    public boolean validPalindrome(String s) {
        int left = 0, right = s.length() - 1;

        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                // 尝试删除左指针指向的字符
                if (isPalindrome(s, left + 1, right)) {
                    return true;
                }
                // 尝试删除右指针指向的字符
                if (isPalindrome(s, left, right - 1)) {
                    return true;
                }
                // 如果删除一个字符后都不能构成回文串，直接返回 false
                return false;
            }

            left++;
            right--;
        }

        return true;
    }

    private boolean isPalindrome(String s, int left, int right) {
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
}
```

这个算法的时间复杂度是 O(n)，其中 n 是字符串 s 的长度。在最坏情况下，需要遍历字符串的一半。