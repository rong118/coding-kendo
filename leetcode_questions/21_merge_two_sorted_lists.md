# 21. Merge Two Sorted Lists

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/merge-two-sorted-lists/)

## Question Description
You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists into one **sorted** list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

Example 1:

> Input: list1 = [1,2,4], list2 = [1,3,4]
>
> Output: [1,1,2,3,4,4]

Example 2:

> Input: list1 = [], list2 = []
>
> Output: []

Example 3:

> Input: list1 = [], list2 = [0]
>
> Output: [0]

Constraints:

* The number of nodes in both lists is in the range [0, 50].
* -100 <= Node.val <= 100
* Both list1 and list2 are sorted in **non-decreasing** order.

## Tags
- linkedlist

## Approach
**Key idea:** The smallest remaining node is always at the head of one of the two lists, so repeatedly splice the smaller head onto the result.

1. Create a dummy node and a `tail` pointer to build the merged list.
2. While both lists are non-empty, attach the node with the smaller value to `tail` and advance that list.
3. Move `tail` forward after each attachment.
4. When one list runs out, attach the rest of the other list (it is already sorted) and return `dummy.next`.

## Code Implementation
```python
from typing import Optional

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = tail = ListNode(0)

        while list1 and list2:
            if list1.val <= list2.val:
                tail.next = list1
                list1 = list1.next
            else:
                tail.next = list2
                list2 = list2.next
            tail = tail.next

        # Attach any remaining nodes
        tail.next = list1 or list2
        return dummy.next
```

## Time Complexity Analysis
> Time complexity  : O(m + n) — single pass through both lists
>
> Space complexity : O(1) — reuses existing nodes

## Related Problems
- [23. Merge k Sorted Lists](./23_merge_k_sorted_lists.md) — 🔴 Hard · generalizes the merge to k lists
- [88. Merge Sorted Array](./88_merge_sorted_array.md) — 🟢 Easy · same merge step on arrays
- [148. Sort List](https://leetcode.com/problems/sort-list) — 🟡 Medium · merge sort built on this merge
