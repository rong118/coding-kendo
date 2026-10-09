# 25. Reverse Nodes in k-Group

**Difficulty:** 🔴 Hard

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

## Approach
**Key idea:** Solve the rest of the list recursively first, then reverse the current group of `k` nodes so its old head points at the already-processed remainder.

1. Walk `k` nodes ahead from `head`; if the list runs out first, return `head` unchanged (the leftover tail stays as is).
2. Recursively process the list starting at the `(k+1)`-th node; its returned head becomes `prev`.
3. Reverse the current `k` nodes one by one, pointing each node at `prev`.
4. After `k` steps, `prev` is the new head of this group — return it.

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

## Related Problems
- [206. Reverse Linked List](./206_reverse_linked_list.md) — 🟢 Easy · the basic in-place reversal used per group
- [92. Reverse Linked List II](./92_reverse_linked_list_II.md) — 🟡 Medium · reverse a sub-range of the list
- [24. Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs) — 🟡 Medium · the k = 2 special case
