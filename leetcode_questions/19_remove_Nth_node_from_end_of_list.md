# 19. Remove Nth Node From End of List

## Question link
(https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

## Question Description
Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

Example 1:

> Input: head = [1,2,3,4,5], n = 2
>
> Output: [1,2,3,5]

Example 2:

> Input: head = [1], n = 1
>
> Output: []

Example 3:

> Input: head = [1,2], n = 1
>
> Output: [1]

Constraints:

* The number of nodes in the list is sz.
* 1 <= sz <= 30
* 0 <= Node.val <= 100
* 1 <= n <= sz

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
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(next=head)
        first = second = dummy

        # Advance first pointer n+1 steps ahead
        for _ in range(n + 1):
            first = first.next

        # Move both until first reaches the end;
        # second lands just before the target node
        while first:
            first = first.next
            second = second.next

        second.next = second.next.next
        return dummy.next
```

## Time Complexity Analysis
> Time complexity  : O(n) — single pass with gap pointer
>
> Space complexity : O(1) — dummy + two pointers
