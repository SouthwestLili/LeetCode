# 59. Spiral Matrix II

## Problem Description

Given a positive integer `n`, generate an `n x n` square matrix filled with all numbers from `1` to `n^2`, arranged in a **clockwise spiral order**.

---

## Example

**Input:**  
n = 3

**Output:**  
[
  [1, 2, 3],
  [8, 9, 4],
  [7, 6, 5]
]

**LeetCode Link:** https://leetcode.com/problems/spiral-matrix-ii/

---

## Spiral Matrix Generation (Layer-by-Layer Simulation)

```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        nums = [[0] * n for _ in range(n)]

        startx, starty = 0, 0          # Starting position
        loop, mid = n // 2, n // 2     # Number of layers, middle index
        count = 1                      # Counter

        for offset in range(1, loop + 1):

            # Left → Right
            for i in range(starty, n - offset):
                nums[startx][i] = count
                count += 1

            # Top → Bottom
            for i in range(startx, n - offset):
                nums[i][n - offset] = count
                count += 1

            # Right → Left
            for i in range(n - offset, starty, -1):
                nums[n - offset][i] = count
                count += 1

            # Bottom → Top
            for i in range(n - offset, startx, -1):
                nums[i][starty] = count
                count += 1

            startx += 1
            starty += 1

        # Fill center for odd n
        if n % 2 != 0:
            nums[mid][mid] = count

        return nums
```

## (Version 2) Boundary-Based Simulation

```python
class Solution(object):
    def generateMatrix(self, n):
        if n <= 0:
            return []

        # Initialize n x n matrix
        matrix = [[0] * n for _ in range(n)]

        # Define boundaries
        top, bottom = 0, n - 1
        left, right = 0, n - 1

        num = 1

        while top <= bottom and left <= right:

            # Left → Right (top row)
            for i in range(left, right + 1):
                matrix[top][i] = num
                num += 1
            top += 1

            # Top → Bottom (right column)
            for i in range(top, bottom + 1):
                matrix[i][right] = num
                num += 1
            right -= 1

            # Right → Left (bottom row)
            for i in range(right, left - 1, -1):
                matrix[bottom][i] = num
                num += 1
            bottom -= 1

            # Bottom → Top (left column)
            for i in range(bottom, top - 1, -1):
                matrix[i][left] = num
                num += 1
            left += 1

        return matrix
```