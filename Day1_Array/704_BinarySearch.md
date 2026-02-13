# 704. Binary Search

## Problem Description

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return -1.

You must write an algorithm with O(log n) runtime complexity.

### Example 1

**Input:** `nums = [-1,0,3,5,9,12], target = 9`  
**Output:** `4`  
**Explanation:** 9 exists in nums and its index is 4

### Example 2

**Input:** `nums = [-1,0,3,5,9,12], target = 2`  
**Output:** `-1`  
**Explanation:** 2 does not exist in nums so return -1

### Constraints

- \( 1 \leq \text{nums.length} \leq 10^4 \)
- \( -10^4 < \text{nums}[i], \text{target} < 10^4 \)
- All integers in `nums` are unique
- `nums` is sorted in ascending order

**LeetCode Link:**  
https://leetcode.com/problems/binary-search/

---

The premise of this problem is that the array is **sorted**. The problem also emphasizes that there are **no duplicate elements**, because once duplicates exist, the index returned by binary search may no longer be unique. These are the fundamental preconditions for applying binary search.

When implementing binary search, there are typically two common interval definitions:

- **Left-closed, right-closed:** `[left, right]`
- **Left-closed, right-open:** `[left, right)`

---

## Left-closed, Right-closed: `[left, right]`

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1          # target is in [left, right]

        while left <= right:
            middle = left + (right - left) // 2

            if nums[middle] > target:
                right = middle - 1              # target in [left, middle - 1]
            elif nums[middle] < target:
                left = middle + 1               # target in [middle + 1, right]
            else:
                return middle                   # target found

        return -1                               # target not found
```

## Left-closed, Right-open: `[left, right)`

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums)              # target is in [left, right)

        while left < right:                     # left == right → empty interval
            middle = left + (right - left) // 2

            if nums[middle] > target:
                right = middle                  # target in [left, middle)
            elif nums[middle] < target:
                left = middle + 1               # target in [middle + 1, right)
            else:
                return middle                   # target found

        return -1                               # target not found
```
