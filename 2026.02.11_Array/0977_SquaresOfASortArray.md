# 977. Squares of a Sorted Array

Given an integer array `nums` sorted in **non-decreasing** order, return an array of **the squares of each number** sorted in **non-decreasing** order.

## Problem Description

### Example 1

**Input:**

nums = [-4, -1, 0, 3, 10]

**Output:**

[0, 1, 9, 16, 100]

**Explanation:**

After squaring, the array becomes:

[16, 1, 0, 9, 100]

After sorting, it becomes:

[0, 1, 9, 16, 100]

---

### Example 2

**Input:**

nums = [-7, -3, 2, 3, 11]

**Output:**

[4, 9, 9, 49, 121]

---

### Constraints

- `1 <= nums.length <= 10^4`
- `-10^4 <= nums[i] <= 10^4`
- `nums` is sorted in **non-decreasing** order.

**LeetCode Link:** https://leetcode.com/problems/squares-of-a-sorted-array/

---

## Brute Force (Element Shifting)

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        for i in range(len(nums)):
            nums[i] *= nums[i]
        nums.sort()
        return nums
```

The time complexity is **O(n + n log n)**.  
Since **n log n** dominates **n**, the overall complexity is **O(n log n)**.

## Two Pointers

The array is already sorted. However, after squaring, negative numbers may become the largest values.

Therefore, the maximum squared value must be located at one of the two ends of the array — either the leftmost or the rightmost element, but never in the middle.

At this point, we can apply the **two-pointer technique**.

### Idea

- Let `i` point to the beginning of the array
- Let `j` point to the end of the array
- Create a new array `result` with the same size
- Let `k` point to the last position of `result`

### Rule

- If `A[i]^2 < A[j]^2`:

  `result[k--] = A[j]^2`

- Otherwise:

  `result[k--] = A[i]^2`

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        l, r = 0, len(nums) - 1
        k = len(nums) - 1
        
        # Pre-allocate result array
        res = [0] * len(nums)
        
        while l <= r:
            if nums[l] ** 2 < nums[r] ** 2:
                res[k] = nums[r] ** 2
                r -= 1
            else:
                res[k] = nums[l] ** 2
                l += 1
            
            k -= 1
        
        return res
```

## Brute Force Approach (Sorting + List Comprehension)

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        return sorted(x*x for x in nums)
```

## Two Pointers + List Reversal

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        # Compare absolute values at both ends
        # Append larger squares first (descending order)
        # Reverse the list at the end
        
        new_list = []
        left, right = 0, len(nums) - 1
        
        while left <= right:
            if abs(nums[left]) <= abs(nums[right]):
                new_list.append(nums[right] ** 2)
                right -= 1
            else:
                new_list.append(nums[left] ** 2)
                left += 1
        
        return new_list[::-1]
```

## (Optimized Two-Pointer Version) Three-Step Optimization

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        """
        Core Idea:
        In a sorted array, the largest absolute value must be at one of the ends.
        Compare both ends and insert the larger square at the back of the new array.

        Optimizations:
        1. Handle special cases (all non-negative / all non-positive)
        2. Replace square comparison with sign comparison (nums[i] + nums[j])
        3. Fill the result array using reverse indexing
        """

        # Special case: all numbers are non-negative (Optimization 1)
        if nums[0] >= 0:
            return [num ** 2 for num in nums]

        # Special case: all numbers are non-positive (Optimization 1)
        if nums[-1] <= 0:
            return [x ** 2 for x in nums[::-1]]

        # General case: mix of negative and positive values
        i, j = 0, len(nums) - 1
        new_nums = [0] * len(nums)

        # Reverse insertion (Optimization 3)
        for end_index in range(len(nums) - 1, -1, -1):

            # Compare via sign instead of squares (Optimization 2)
            if nums[i] + nums[j] <= 0:
                new_nums[end_index] = nums[i] ** 2
                i += 1
            else:
                new_nums[end_index] = nums[j] ** 2
                j -= 1

        return new_nums
```