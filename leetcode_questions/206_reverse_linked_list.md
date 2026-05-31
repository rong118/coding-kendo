# 206. Reverse Linked List

## Question link
(https://leetcode.com/problems/reverse-linked-list/)

## Question Description
Given the `head` of a singly linked list, reverse the list, and return the reversed list.

Example 1:

> Input: head = [1,2,3,4,5]
>
> Output: [5,4,3,2,1]

Example 2:

> Input: head = [1,2]
>
> Output: [2,1]

Example 3:

> Input: head = []
>
> Output: []

Constraints:

* The number of nodes in the list is the range [0, 5000].
* -5000 <= Node.val <= 5000

**Follow up**: A linked list can be reversed either iteratively or recursively. Could you implement both?

## Tags
- linkedlist

## Code Implementation
```python
from typing import Optional

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    # Iterative — reverse pointers in one pass
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        cur = head
        while cur:
            nxt = cur.next
            cur.next = prev
            prev = cur
            cur = nxt
        return prev

    # Recursive — unwind and relink from the tail
    def reverseListRecursive(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or not head.next:
            return head
        new_head = self.reverseListRecursive(head.next)
        head.next.next = head
        head.next = None
        return new_head
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node visited once
>
> Space complexity : O(1) iterative, O(n) recursive (call stack)
