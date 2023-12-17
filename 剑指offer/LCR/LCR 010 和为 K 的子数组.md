给定一个整数数组和一个整数 `k` **，**请找到该数组中和为 `k` 的连续子数组的个数。

 

**示例 1：**

```
输入:nums = [1,1,1], k = 2
输出: 2
解释: 此题 [1,1] 与 [1,1] 为两种不同的情况
```

**示例 2：**

```
输入:nums = [1,2,3], k = 3
输出: 2
```

 

**提示:**

- `1 <= nums.length <= 2 * 104`
- `-1000 <= nums[i] <= 1000`
- `-107 <= k <= 107`





题目链接：

https://leetcode.cn/problems/QTMn0o/







这道题目可以通过使用前缀和（prefix sum）的方法来解决。具体步骤如下：

1. **计算前缀和数组**：首先，创建一个额外的数组 `prefixSum`，用于存储从数组开始到当前位置的元素和。`prefixSum[i]` 表示数组 `nums` 中前 i 个元素的和。

2. **遍历计算子数组和**：接下来，使用两层循环遍历数组，分别选择子数组的起始位置 `i` 和结束位置 `j`，然后计算从 `i` 到 `j` 的子数组和。子数组和可以通过 `prefixSum[j] - prefixSum[i] + nums[i]` 计算得到。

3. **统计符合条件的子数组个数**：在计算子数组和的过程中，统计满足和为 `k` 的子数组个数。

4. **返回结果**：返回最终的统计结果。

以下是相应的Java代码：

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int n = nums.length;
        
        // 计算前缀和数组
        int[] prefixSum = new int[n + 1];
        for (int i = 0; i < n; i++) {
            prefixSum[i + 1] = prefixSum[i] + nums[i];
        }

        // 遍历计算子数组和并统计符合条件的子数组个数
        int count = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j <= n; j++) {
                if (prefixSum[j] - prefixSum[i] == k) {
                    count++;
                }
            }
        }

        return count;
    }
}
```

上述代码的时间复杂度为 O(n^2)，其中 n 是数组的长度。在实际应用中，还可以通过优化算法来减少时间复杂度。