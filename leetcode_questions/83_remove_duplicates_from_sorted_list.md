# 83. Remove Duplicates from Sorted List

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
