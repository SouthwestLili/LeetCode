# 24. Swap Nodes in Pairs

## Problem Description

Given a linked list, swap every two adjacent nodes and return the modified list.

**Constraint:**
You may not simply change the values inside the nodes — you must actually swap the nodes themselves.

## Recursive Version

### Idea

Use recursion to swap the first two nodes, then recursively process the rest of the list.

### Base Case

If the list is empty or contains only one node, no swap is needed.

**LeetCode Link:** https://leetcode.com/problems/swap-nodes-in-pairs/description/

### Recursive Case

1. Identify the two nodes to swap  
2. Swap them  
3. Recursively swap the remaining list  

### Implementation

```python
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head is None or head.next is None:
            return head

        # Nodes to be swapped
        pre = head
        cur = head.next
        next_node = head.next.next
        
        # Swap
        cur.next = pre
        
        # Recursively swap remaining list
        pre.next = self.swapPairs(next_node)
         
        return cur
```

### Complexity

**Time Complexity:** O(n)  
Each node is visited once.

**Space Complexity:** O(n)  
Extra space is used by the recursion call stack.

## Iterative Version (Dummy Head)

### Idea

Use a dummy head node to simplify pointer manipulation.  
Iteratively swap pairs while traversing the list.

### Key Insight

To perform a swap, we must have **two nodes available**:


If this condition fails, no further swaps are possible.

### Implementation

```python
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        dummy_head = ListNode(next=head)
        current = dummy_head
        
        while current.next and current.next.next:
            # Nodes involved in swap
            first = current.next
            second = current.next.next
            next_pair = second.next
            
            # Swap
            current.next = second
            second.next = first
            first.next = next_pair
            
            # Move to next pair
            current = first
            
        return dummy_head.next

```

### Why Dummy Head?

Without a dummy node, swapping the first pair requires special-case logic  
because the head pointer itself changes.

A dummy head:

- Eliminates edge cases  
- Keeps pointer manipulation consistent  
- Simplifies the implementation  

---

### Complexity

**Time Complexity:** O(n)  
Each node is processed once.

**Space Complexity:** O(1)  
No extra memory is used (in-place swapping).
