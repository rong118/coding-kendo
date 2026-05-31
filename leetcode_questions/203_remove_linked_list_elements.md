# 203. Remove Linked List Elements

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
