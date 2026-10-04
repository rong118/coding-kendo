# 142. Linked List Cycle II

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/linked-list-cycle-ii/)

## Question Description
Given the `head` of a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to (**0-indexed**). It is `-1` if there is no cycle. **Note that `pos` is not passed as a parameter.**

**Do not modify** the linked list.

Example 1:

> Input: head = [3,2,0,-4], pos = 1
>
> Output: tail connects to node index 1
>
> Explanation: There is a cycle in the linked list, where tail connects to the second node.

Example 2:

> Input: head = [1,2], pos = 0
>
> Output: tail connects to node index 0
>
> Explanation: There is a cycle in the linked list, where tail connects to the first node.

Example 3:

> Input: head = [1], pos = -1
>
> Output: no cycle
>
> Explanation: There is no cycle in the linked list.

Constraints:

* The number of the nodes in the list is in the range [0, 10^4].
* -10^5 <= Node.val <= 10^5
* pos is -1 or a valid index in the linked-list.

## Tags
- linkedlist

## Approach
**Key idea:** With Floyd's tortoise and hare, once the pointers meet inside the cycle, the distance from the head to the cycle entry equals the distance from the meeting point to the entry (mod the cycle length).

1. Move `slow` one step and `fast` two steps at a time.
2. If `fast` reaches the end, there is no cycle — return `None`.
3. When `slow` and `fast` meet, restart a pointer from `head`.
4. Advance both pointers one step at a time; the node where they meet is the cycle entry.

## Code Implementation
```python
from typing import Optional

class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow = fast = head

        # Phase 1: detect cycle with Floyd's algorithm
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                # Phase 2: find entry point — distance from head to entry
                # equals distance from meeting point to entry
                while head != fast:
                    head = head.next
                    fast = fast.next
                return fast

        return None
```

## Time Complexity Analysis
> Time complexity  : O(n) — phase 1 visits ≤ n nodes, phase 2 visits ≤ n nodes
>
> Space complexity : O(1) — only two pointers

## Related Problems
- [141. Linked List Cycle](./141_linked_list_cycle.md) — 🟢 Easy · phase 1 of the same Floyd algorithm
- [287. Find the Duplicate Number](./287_find_the_duplicate_number.md) — 🟡 Medium · cycle entry detection on an index-linked array
- [160. Intersection of Two Linked Lists](./160_intersection_of_two_linked_lists.md) — 🟢 Easy · two pointers converging on a shared node
