# 206. Reverse Linked List

## Problem Description

Reverse a singly linked list.

**Example:**

Input:  
1 -> 2 -> 3 -> 4 -> 5 -> NULL

Output:  
5 -> 4 -> 3 -> 2 -> 1 -> NULL

**LeetCode Link:** https://leetcode.com/problems/reverse-linked-list/

---

### (Version 1) Two-Pointer Technique

```python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        cur = head
        pre = None

        while cur:
            temp = cur.next      # Store next node
            cur.next = pre       # Reverse pointer

            pre = cur            # Move pre forward
            cur = temp           # Move cur forward

        return pre
```

### (Version 2) Recursive Approach

```python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        return self.reverse(head, None)

    def reverse(self, cur: ListNode, pre: ListNode) -> ListNode:
        if cur is None:
            return pre

        temp = cur.next      # Store next node
        cur.next = pre       # Reverse pointer

        return self.reverse(temp, cur)
```