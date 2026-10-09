# 83. Remove Duplicates from Sorted List

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/remove-duplicates-from-sorted-list/)

## Question Description
Given the `head` of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list **sorted** as well.

Example 1:

> Input: head = [1,1,2]
>
> Output: [1,2]

Example 2:

> Input: head = [1,1,2,3,3]
>
> Output: [1,2,3]

Constraints:

* The number of nodes in the list is in the range [0, 300].
* -100 <= Node.val <= 100
* The list is guaranteed to be **sorted in ascending order**.

## Tags
- linkedlist

## Approach
**Key idea:** Because the list is sorted, all duplicates of a value are adjacent, so each node only needs to be compared with its next node.

1. Start `cur` at `head`.
2. While `cur` and `cur.next` exist, compare their values.
3. If equal, skip the duplicate with `cur.next = cur.next.next` (stay on `cur` to catch longer runs).
4. Otherwise advance `cur`; return `head` when done.

## Code Implementation
```python
from typing import Optional

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        cur = head
        while cur and cur.next:
            if cur.val == cur.next.val:
                cur.next = cur.next.next  # skip duplicate
            else:
                cur = cur.next
        return head
```

## Time Complexity Analysis
> Time complexity  : O(n) — single pass through the sorted list
>
> Space complexity : O(1) — in-place pointer updates

## Related Problems
- [82. Remove Duplicates from Sorted List II](./82_remove_duplicates_from_sorted_list_II.md) — 🟡 Medium · follow-up that removes every duplicated value entirely
- [26. Remove Duplicates from Sorted Array](./26_remove_duplicates_from_sorted_array.md) — 🟢 Easy · same idea on an array with two pointers
- [203. Remove Linked List Elements](./203_remove_linked_list_elements.md) — 🟢 Easy · in-place node unlinking
