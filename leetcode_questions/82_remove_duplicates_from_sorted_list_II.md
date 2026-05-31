# 82. Remove Duplicates from Sorted List II

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
