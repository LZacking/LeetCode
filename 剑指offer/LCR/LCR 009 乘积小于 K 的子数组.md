给定一个正整数数组 `nums`和整数 `k` ，请找出该数组内乘积小于 `k` 的连续的子数组的个数。

 

**示例 1:**

```
输入: nums = [10,5,2,6], k = 100
输出: 8
解释: 8 个乘积小于 100 的子数组分别为: [10], [5], [2], [6], [10,5], [5,2], [2,6], [5,2,6]。
需要注意的是 [10,5,2] 并不是乘积小于100的子数组。
```

**示例 2:**

```
输入: nums = [1,2,3], k = 0
输出: 0
```

 

**提示:** 

- `1 <= nums.length <= 3 * 104`
- `1 <= nums[i] <= 1000`
- `0 <= k <= 106`

 

注意：本题与主站 713 题相同：<https://leetcode-cn.com/problems/subarray-product-less-than-k/> 



题目链接：

https://leetcode.cn/problems/ZVAVXX/





**分析：**

题目要求找出数组中乘积小于 k 的连续子数组的个数。可以使用滑动窗口的思想解决此问题。通过维护窗口的起始位置和结束位置，不断调整窗口大小，以满足条件。

**解题步骤：**

1. 初始化窗口的起始位置和结束位置为 0。
2. 使用双指针维护滑动窗口，移动右指针以扩大窗口，直到子数组的乘积小于 k。
3. 计算当前窗口的长度，并更新结果。
4. 移动左指针，缩小窗口，直到子数组的乘积大于等于 k。
5. 不断重复步骤 2 到 4，直到右指针到达数组末尾。

**Java代码实现：**

```java
class Solution {
    public int numSubarrayProductLessThanK(int[] nums, int k) {
        if (k <= 1) {
            return 0;  // 乘积小于等于 0 的子数组不存在
        }

        int left = 0; // 窗口的左指针
        int product = 1;  // 当前窗口的乘积
        int count = 0;

        for (int right = 0; right < nums.length; right++) {
            product *= nums[right];

            // 当窗口乘积大于等于 k 时，缩小窗口
            while (product >= k) {
                product /= nums[left];
                left++;
            }

            // 计算当前窗口的长度，并累加到结果中
            count += right - left + 1;
        }

        return count;
    }
}
```

这段代码使用了滑动窗口的思想，时间复杂度为 O(n)，其中 n 是数组的长度。