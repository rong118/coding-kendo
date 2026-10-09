# 82. Remove Duplicates from Sorted List II

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/)

## Question Description
Given the `head` of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list **sorted** as well.

Example 1:

> Input: head = [1,2,3,3,4,4,5]
>
> Output: [1,2,5]

Example 2:

> Input: head = [1,1,1,2,3]
>
> Output: [2,3]

Constraints:

* The number of nodes in the list is in the range [0, 300].
* -100 <= Node.val <= 100
* The list is guaranteed to be **sorted in ascending order**.

## Tags
- linkedlist

## Approach
**Key idea:** A dummy node in front of `head` lets us delete a run of duplicates even when it starts at the head; `prev` always points at the last node known to be distinct.

1. Create `dummy -> head`, set `prev = dummy` and `cur = head`.
2. If `cur` and `cur.next` share a value, advance `cur` past every node with that value and link `prev.next = cur`.
3. Otherwise `cur` is distinct: move both `prev` and `cur` one step forward.
4. Return `dummy.next`.

## Code Implementation
```python
from typing import Optional

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(next=head)
        prev = dummy
        cur = head

        while cur:
            # If a duplicate sequence is found, skip all nodes with that value
            if cur.next and cur.val == cur.next.val:
                val = cur.val
                while cur and cur.val == val:
                    cur = cur.next
                prev.next = cur
            else:
                prev = prev.next
                cur = cur.next

        return dummy.next
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node visited once
>
> Space complexity : O(1) — in-place with a single dummy node

## Related Problems
- [83. Remove Duplicates from Sorted List](./83_remove_duplicates_from_sorted_list.md) — 🟢 Easy · keep one copy instead of removing all
- [203. Remove Linked List Elements](./203_remove_linked_list_elements.md) — 🟢 Easy · dummy-node deletion in a linked list
- [26. Remove Duplicates from Sorted Array](./26_remove_duplicates_from_sorted_array.md) — 🟢 Easy · same dedup on a sorted array
