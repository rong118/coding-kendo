# 141. Linked List Cycle

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/linked-list-cycle/)

## Question Description
Given `head`, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to. **Note that `pos` is not passed as a parameter.**

Return `true` if there is a cycle in the linked list. Otherwise, return `false`.

Example 1:

> Input: head = [3,2,0,-4], pos = 1
>
> Output: true
>
> Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

Example 2:

> Input: head = [1,2], pos = 0
>
> Output: true
>
> Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.

Example 3:

> Input: head = [1], pos = -1
>
> Output: false
>
> Explanation: There is no cycle in the linked list.

Constraints:

* The number of the nodes in the list is in the range [0, 10^4].
* -10^5 <= Node.val <= 10^5
* pos is -1 or a valid index in the linked-list.

## Tags
- linkedlist

## Approach
**Key idea:** Floyd's tortoise and hare — a fast pointer moving two steps will eventually lap a slow pointer moving one step if and only if there is a cycle.

1. Start `slow` and `fast` at `head`.
2. While `fast` and `fast.next` exist, move `slow` one step and `fast` two steps.
3. If they ever point to the same node, a cycle exists — return `True`.
4. If `fast` reaches the end of the list, there is no cycle — return `False`.

## Code Implementation
```python
from typing import Optional

class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow = fast = head

        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True

        return False
```

## Time Complexity Analysis
> Time complexity  : O(n) — at most one full traversal before fast catches slow
>
> Space complexity : O(1) — only two pointers

## Related Problems
- [142. Linked List Cycle II](./142_linked_list_cycle_II.md) — 🟡 Medium · also find where the cycle starts
- [287. Find the Duplicate Number](./287_find_the_duplicate_number.md) — 🟡 Medium · Floyd's cycle detection on an array
- [160. Intersection of Two Linked Lists](./160_intersection_of_two_linked_lists.md) — 🟢 Easy · two-pointer trick on linked lists
