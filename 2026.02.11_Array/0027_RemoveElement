# 27. Remove Element

## Problem Description

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` **in-place**. The order of the elements may be changed.

Return the number of elements in `nums` which are **not equal to `val`**.

Let `k` be the number of elements in `nums` that are not equal to `val`.

To be accepted, you must:

- Change the array `nums` such that the first `k` elements of `nums` contain the elements which are not equal to `val`. The remaining elements of `nums` are not important as well as the size of `nums`.
- Return `k`.

---

## Example 1

**Input:**  
nums = [3,2,2,3], val = 3  

**Output:**  
2, nums = [2,2,_,_]

**Explanation:**  
Your function should return `k = 2`, with the first two elements being `2`.  
Elements beyond `k` do not matter.

---

## Example 2

**Input:**  
nums = [0,1,2,2,3,0,4,2], val = 2  

**Output:**  
5, nums = [0,1,4,0,3,_,_,_]

**Explanation:**  
Your function should return `k = 5`, with the first five elements containing  
`0, 0, 1, 3, 4` (any order is acceptable).

---

## Constraints

- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= val <= 100`

**LeetCode link:** https://leetcode.com/problems/remove-element/description/

---

## Fast & Slow Pointer (Two-Pointer Technique)

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        # Fast & slow pointers
        fast = 0                        # Fast pointer
        slow = 0                        # Slow pointer
        size = len(nums)

        # We use fast < size (not <=) to avoid index out of bounds
        while fast < size:
            # The slow pointer collects values not equal to val
            # If nums[fast] != val, copy it to nums[slow]
            if nums[fast] != val:
                nums[slow] = nums[fast]
                slow += 1

            fast += 1

        return slow
```

### Idea: Two-Pointer Approach

- fast scans every element

- slow marks the position to write valid elements

- Overwrites unwanted values in-place

#### Complexity

- Time: O(n)

- Space: O(1)

---

## Brute Force (Element Shifting)

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        i, l = 0, len(nums)

        while i < l:
            if nums[i] == val:          # Found target value
                # Shift elements left
                for j in range(i + 1, l):
                    nums[j - 1] = nums[j]

                l -= 1                  # Reduce array length
                i -= 1                  # Recheck current index

            i += 1

        return l
```

### Idea: Brute Force Shifting

- When target found → shift remaining elements forward

- Repeated shifting causes extra work

#### Complexity

- Time: O(n²) (worst case)

- Space: O(1)

---

## Opposite Direction Two Pointers

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        n = len(nums)
        left, right = 0, n - 1

        while left <= right:

            # Move left pointer until target found
            while left <= right and nums[left] != val:
                left += 1

            # Move right pointer until valid value found
            while left <= right and nums[right] == val:
                right -= 1

            # Replace target with valid value
            if left < right:
                nums[left] = nums[right]
                left += 1
                right -= 1

        return left
```

### Idea: Bidirectional Pointers

- left searches for elements to remove

- right searches for elements to keep

- Swap/remove efficiently

#### Complexity

- Time: O(n)

- Space: O(1)

--- 

## Summary Comparison

            | Approach              | Time Complexity | Space Complexity | Notes                       |
            | --------------------- | --------------- | ---------------- | --------------------------- |
            | Fast & Slow Pointer   | **O(n)**        | **O(1)**         | Most common & stable        |
            | Brute Force           | **O(n²)**       | **O(1)**         | Inefficient due to shifting |
            | Opposite Two Pointers | **O(n)**        | **O(1)**         | Order may change            |
