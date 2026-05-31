# 25. Reverse Nodes in k-Group

## Question link
(https://leetcode.com/problems/reverse-nodes-in-k-group/)

## Question Description
Given the `head` of a linked list, reverse the nodes of the linked list `k` at a time and return its modified list.

`k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes — only nodes themselves may be changed.

Example 1:

> Input: head = [1,2,3,4,5], k = 2
>
> Output: [2,1,4,3,5]

Example 2:

> Input: head = [1,2,3,4,5], k = 3
>
> Output: [3,2,1,4,5]

Constraints:

* The number of nodes in the list is n.
* 1 <= k <= n <= 5000
* 0 <= Node.val <= 1000

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
    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        # Count k nodes ahead — if fewer than k, return head unchanged
        node = head
        count = 0
        while count < k:
            if not node:
                return head
            node = node.next
            count += 1

        # Reverse the first k nodes
        prev = self.reverseKGroup(node, k)
        while count > 0:
            nxt = head.next
            head.next = prev
            prev = head
            head = nxt
            count -= 1

        return prev
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node visited twice (count + reverse)
>
> Space complexity : O(n/k) — recursion depth proportional to number of groups
