# 206. Reverse Linked List

**Difficulty:** 🟢 Easy

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

## Approach
**Key idea:** Walk the list once and flip each `next` pointer to point at the previous node; the old tail becomes the new head.

1. Keep `prev = None` and `cur = head`.
2. Save `cur.next`, point `cur.next` back to `prev`.
3. Advance `prev` to `cur` and `cur` to the saved next node.
4. When `cur` is `None`, `prev` is the new head.
5. Recursive variant: reverse the rest of the list, then make `head.next.next = head` and cut `head.next`.

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

## Related Problems
- [92. Reverse Linked List II](./92_reverse_linked_list_II.md) — 🟡 Medium · reverse only a sub-range of the list
- [25. Reverse Nodes in k-Group](./25_reverse_nodes_in_k_group.md) — 🔴 Hard · repeated in-place reversal of k-sized chunks
- [234. Palindrome Linked List](./234_palindrome_linked_list.md) — 🟢 Easy · reverse the second half to compare
