# 1171. Remove Zero Sum Consecutive Nodes from Linked List

## Question link
(https://leetcode.com/problems/remove-zero-sum-consecutive-nodes-from-linked-list/)

## Question Description
Given the `head` of a linked list, we repeatedly delete consecutive sequences of nodes that sum to `0` until there are no such sequences.

After doing so, return the head of the final linked list. You may return any such answer.

(Note that in the examples below, all sequences are serializations of `ListNode` objects.)

Example 1:

> Input: head = [1,2,-3,3,1]
>
> Output: [3,1]
>
> Note: The answer [1,2,1] would also be accepted.

Example 2:

> Input: head = [1,2,3,-3,4]
>
> Output: [1,2,4]

Example 3:

> Input: head = [1,2,3,-3,-2]
>
> Output: [1]

Constraints:

* The given linked list will contain between `1` and `1000` nodes.
* Each node in the linked list has `-1000 <= node.val <= 1000`.

## Tags
- linkedlist
- prefix-sum

## Code Implementation
```python
from typing import Optional

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def removeZeroSumSublists(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        prefix = 0
        seen = {0: dummy}  # prefix sum → last node with that sum

        # First pass: record the last occurrence of each prefix sum.
        # When the same prefix sum appears again, the nodes in between
        # sum to zero and the later entry overwrites the earlier one,
        # effectively skipping the zero-sum segment.
        cur = dummy
        while cur:
            prefix += cur.val
            seen[prefix] = cur
            cur = cur.next

        # Second pass: skip zero-sum segments using the stored positions
        cur = dummy
        prefix = 0
        while cur:
            prefix += cur.val
            cur.next = seen[prefix].next
            cur = cur.next

        return dummy.next
```

## Time Complexity Analysis
> Time complexity  : O(n) — two passes through the list
>
> Space complexity : O(n) — hash map stores at most n prefix sums
