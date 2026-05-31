# 160. Intersection of Two Linked Lists

## Question link
(https://leetcode.com/problems/intersection-of-two-linked-lists/)

## Question Description
Given the heads of two singly linked-lists `headA` and `headB`, return the node at which the two lists intersect. If the two linked lists have no intersection at all, return `null`.

The test cases are generated such that there are **no cycles** anywhere in the entire linked structure.

**Note** that the linked lists must **retain their original structure** after the function returns.

Example 1:

> Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,6,1,8,4,5], skipA = 2, skipB = 3
>
> Output: Intersected at '8'

Example 2:

> Input: intersectVal = 2, listA = [1,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
>
> Output: Intersected at '2'

Example 3:

> Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
>
> Output: No intersection

Constraints:

* The number of nodes of listA is m, listB is n.
* 1 <= m, n <= 3 * 10^4
* 1 <= Node.val <= 10^5
* intersectVal is 0 if listA and listB do not intersect.
* intersectVal == listA[skipA] == listB[skipB] if they intersect.

**Follow up**: Could you write a solution that runs in O(m + n) time and use only O(1) memory?

## Tags
- linkedlist

## Code Implementation
```python
from typing import Optional

class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        a, b = headA, headB

        # When a pointer reaches the end of its list, redirect to the head
        # of the other list. If they intersect, they will meet at the
        # intersection node after at most one full cycle each.
        # Logic: a + c + b = b + c + a (same total distance travelled)
        while a != b:
            a = a.next if a else headB
            b = b.next if b else headA

        return a
```

## Time Complexity Analysis
> Time complexity  : O(m + n) — each pointer traverses both lists at most once
>
> Space complexity : O(1) — only two pointers
