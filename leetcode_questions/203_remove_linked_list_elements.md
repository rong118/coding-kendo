# 203. Remove Linked List Elements

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/remove-linked-list-elements/)

## Question Description
Given the `head` of a linked list and an integer `val`, remove all the nodes of the linked list that has `Node.val == val`, and return the new head.

Example 1:

> Input: head = [1,2,6,3,4,5,6], val = 6
>
> Output: [1,2,3,4,5]

Example 2:

> Input: head = [], val = 1
>
> Output: []

Example 3:

> Input: head = [7,7,7,7], val = 7
>
> Output: []

Constraints:

* The number of nodes in the list is in the range [0, 10^4].
* 1 <= Node.val <= 50
* 0 <= val <= 50

## Tags
- linkedlist

## Approach
**Key idea:** A dummy node in front of the head means the head is just another "next" pointer, so removing it needs no special case.

1. Create `dummy` pointing at `head` and set `cur = dummy`.
2. While `cur.next` exists, check its value.
3. If `cur.next.val == val`, unlink it with `cur.next = cur.next.next` (stay on `cur` to check the new next node).
4. Otherwise advance `cur`.
5. Return `dummy.next`. (The recursive version cleans the tail first, then decides whether to keep the current node.)

## Code Implementation
```python
from typing import Optional

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    # Iterative — dummy node simplifies head-removal edge case
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        dummy = ListNode(next=head)
        cur = dummy
        while cur.next:
            if cur.next.val == val:
                cur.next = cur.next.next
            else:
                cur = cur.next
        return dummy.next

    # Recursive — process from the tail backward
    def removeElementsRecursive(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        if not head:
            return None
        head.next = self.removeElementsRecursive(head.next, val)
        return head.next if head.val == val else head
```

## Time Complexity Analysis
> Time complexity  : O(n) — single pass through the list
>
> Space complexity : O(1) iterative, O(n) recursive (call stack)

## Related Problems
- [83. Remove Duplicates from Sorted List](./83_remove_duplicates_from_sorted_list.md) — 🟢 Easy · unlinking nodes in a single pass
- [82. Remove Duplicates from Sorted List II](./82_remove_duplicates_from_sorted_list_II.md) — 🟡 Medium · dummy node for possible head removal
- [19. Remove Nth Node From End of List](./19_remove_Nth_node_from_end_of_list.md) — 🟡 Medium · dummy node plus pointer unlinking
- [27. Remove Element](./27_remove_element.md) — 🟢 Easy · same task on an array
