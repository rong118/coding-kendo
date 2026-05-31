# 92. Reverse Linked List II

## Question link
(https://leetcode.com/problems/reverse-linked-list-ii/)

## Question Description
Given the `head` of a singly linked list and two integers `left` and `right` where `left <= right`, reverse the nodes of the list from position `left` to position `right`, and return the reversed list.

Example 1:

> Input: head = [1,2,3,4,5], left = 2, right = 4
>
> Output: [1,4,3,2,5]

Example 2:

> Input: head = [5], left = 1, right = 1
>
> Output: [5]

Constraints:

* The number of nodes in the list is n.
* 1 <= n <= 500
* -500 <= Node.val <= 500
* 1 <= left <= right <= n

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
    def reverseBetween(self, head: Optional[ListNode], left: int, right: int) -> Optional[ListNode]:
        dummy = ListNode(next=head)

        # Move pre to the node just before the reversal segment
        pre = dummy
        for _ in range(left - 1):
            pre = pre.next

        # Reverse the sublist between left and right
        cur = pre.next
        for _ in range(right - left):
            nxt = cur.next
            cur.next = nxt.next
            nxt.next = pre.next
            pre.next = nxt

        return dummy.next
```

## Time Complexity Analysis
> Time complexity  : O(n) — single pass, reversing at most n nodes
>
> Space complexity : O(1) — in-place pointer manipulation
