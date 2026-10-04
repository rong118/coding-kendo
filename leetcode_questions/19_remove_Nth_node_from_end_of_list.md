# 19. Remove Nth Node From End of List

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

## Question Description
Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

Example 1:

> Input: head = [1,2,3,4,5], n = 2
>
> Output: [1,2,3,5]

Example 2:

> Input: head = [1], n = 1
>
> Output: []

Example 3:

> Input: head = [1,2], n = 1
>
> Output: [1]

Constraints:

* The number of nodes in the list is sz.
* 1 <= sz <= 30
* 0 <= Node.val <= 100
* 1 <= n <= sz

## Tags
- linkedlist

## Approach
**Key idea:** If one pointer runs `n + 1` nodes ahead of another, then when the leading pointer falls off the end, the trailing pointer sits right before the node to delete.

1. Add a dummy node before `head` so removing the head itself needs no special case.
2. Start `first` and `second` at the dummy and advance `first` by `n + 1` steps.
3. Move both pointers one step at a time until `first` is `None`.
4. Unlink the target with `second.next = second.next.next` and return `dummy.next`.

## Code Implementation
```python
from typing import Optional

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(next=head)
        first = second = dummy

        # Advance first pointer n+1 steps ahead
        for _ in range(n + 1):
            first = first.next

        # Move both until first reaches the end;
        # second lands just before the target node
        while first:
            first = first.next
            second = second.next

        second.next = second.next.next
        return dummy.next
```

## Time Complexity Analysis
> Time complexity  : O(n) — single pass with gap pointer
>
> Space complexity : O(1) — dummy + two pointers

## Related Problems
- [203. Remove Linked List Elements](./203_remove_linked_list_elements.md) — 🟢 Easy · dummy-head trick for deleting nodes
- [876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list) — 🟢 Easy · two pointers at different speeds/offsets
- [141. Linked List Cycle](./141_linked_list_cycle.md) — 🟢 Easy · fast/slow pointer pattern
- [61. Rotate List](https://leetcode.com/problems/rotate-list) — 🟡 Medium · locating the k-th node from the end
