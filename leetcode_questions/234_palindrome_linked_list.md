# 234. Palindrome Linked List

## Question link
(https://leetcode.com/problems/palindrome-linked-list/)

## Question Description
Given the `head` of a singly linked list, return `true` if it is a **palindrome**.

Example 1:

> Input: head = [1,2,2,1]
>
> Output: true

Example 2:

> Input: head = [1,2]
>
> Output: false

Constraints:

* The number of nodes in the list is in the range [1, 10^5].
* 0 <= Node.val <= 9

**Follow up**: Could you do it in O(n) time and O(1) space?

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
    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        # 1. Find the middle with fast/slow pointer
        slow = fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        # 2. Reverse the second half in place
        prev = None
        while slow:
            nxt = slow.next
            slow.next = prev
            prev = slow
            slow = nxt

        # 3. Compare first half and reversed second half
        left, right = head, prev
        while right:
            if left.val != right.val:
                return False
            left = left.next
            right = right.next

        return True
```

## Time Complexity Analysis
> Time complexity  : O(n) — find middle, reverse, compare each traverse at most n nodes
>
> Space complexity : O(1) — in-place reversal, no extra storage
