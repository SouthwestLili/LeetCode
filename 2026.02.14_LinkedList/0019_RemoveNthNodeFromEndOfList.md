# 19. Remove Nth Node From End of List

## Problem Description

Given a linked list, remove the n-th node from the end of the list  
and return the head of the modified list.

## Examples

**Example 1**  
Input: `head = [1,2,3,4,5]`, `n = 2`  
Output: `[1,2,3,5]`

**Example 2**  
Input: `head = [1]`, `n = 1`  
Output: `[]`

**Example 3**  
Input: `head = [1,2]`, `n = 1`  
Output: `[1]`

**LeetCode Link:** https://leetcode.com/problems/remove-nth-node-from-end-of-list/

---

## Solution (Two Pointers)

### Idea

Use the **two-pointer technique**:

- Move the fast pointer ahead by `n + 1` steps
- Then move both pointers together
- When fast reaches the end, slow is right before the node to delete

### Why Move `n + 1` Steps?

This guarantees that:

            distance(fast, slow) = n


So slow stops at the node **before** the target.

### Implementation

```python
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        dummy_head = ListNode(0, head)
        
        slow = fast = dummy_head
        
        # Move fast pointer n+1 steps ahead
        for _ in range(n + 1):
            fast = fast.next
        
        # Move both pointers
        while fast:
            slow = slow.next
            fast = fast.next
        
        # Delete target node
        slow.next = slow.next.next
        
        return dummy_head.next
```

### Complexity

**Time Complexity:** O(n)  
Single traversal of the list.

**Space Complexity:** O(1)  
Only pointer variables are used.
