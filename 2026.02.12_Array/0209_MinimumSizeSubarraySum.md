# 209. Minimum Size Subarray Sum

## Problem Description

Given an array of `n` **positive integers** and a positive integer `s`, find the **minimum length** of a **contiguous subarray** whose sum is **greater than or equal to `s`**, and return its length.  
If there is no such subarray, return `0`.

---

## Example

**Input:**

s = 7, nums = [2, 3, 1, 2, 4, 3]

**Output:**

2

**Explanation:**

The subarray `[4, 3]` has the minimum length under the condition.

---

## Constraints

- `1 <= target <= 10^9`
- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^5`

**LeetCode Link:** https://leetcode.com/problems/minimum-size-subarray-sum/

---

## (Version 1) Sliding Window 

```python
class Solution:
    def minSubArrayLen(self, s: int, nums: List[int]) -> int:
        n = len(nums)
        left = 0
        cur_sum = 0
        min_len = float('inf')

        for right in range(n):
            cur_sum += nums[right]

            while cur_sum >= s:
                min_len = min(min_len, right - left + 1)
                cur_sum -= nums[left]
                left += 1

        return min_len if min_len != float('inf') else 0

```

## (Version 2) Brute Force Approach

```python
class Solution:
    def minSubArrayLen(self, s: int, nums: List[int]) -> int:
        n = len(nums)
        min_len = float('inf')

        for i in range(n):
            cur_sum = 0

            for j in range(i, n):
                cur_sum += nums[j]

                if cur_sum >= s:
                    min_len = min(min_len, j - i + 1)
                    break

        return min_len if min_len != float('inf') else 0
```