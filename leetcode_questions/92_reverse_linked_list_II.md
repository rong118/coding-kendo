# 92. Reverse Linked List II

**Difficulty:** 🟡 Medium

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

## Approach
**Key idea:** Walk to the node just before position `left`, then repeatedly take the node after the current one and move it to the front of the segment. After `right - left` moves the segment is reversed in place.

1. Put a dummy node before `head` so that `left = 1` needs no special case.
2. Move `pre` forward `left - 1` steps; it now sits just before the segment.
3. Let `cur = pre.next` (the first node of the segment, which ends up last).
4. Repeat `right - left` times: unlink `nxt = cur.next` and insert it right after `pre`.
5. Return `dummy.next`.

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

## Related Problems
- [206. Reverse Linked List](./206_reverse_linked_list.md) — 🟢 Easy · reverse the whole list
- [25. Reverse Nodes in k-Group](./25_reverse_nodes_in_k_group.md) — 🔴 Hard · reverse segments in place repeatedly
- [234. Palindrome Linked List](./234_palindrome_linked_list.md) — 🟢 Easy · reverse part of a list in place
