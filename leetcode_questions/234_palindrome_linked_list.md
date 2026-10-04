# 234. Palindrome Linked List

**Difficulty:** 🟢 Easy

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

## Approach
**Key idea:** Reverse the second half of the list in place, then a palindrome reads the same walking forward from the head and from the reversed tail.

1. Use slow/fast pointers to find the middle (`slow` ends at the start of the second half).
2. Reverse the list starting at `slow`; `prev` becomes the head of the reversed half.
3. Walk `head` and `prev` together, returning `False` on the first mismatch.
4. If the reversed half is exhausted without a mismatch, return `True`.

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

## Related Problems
- [206. Reverse Linked List](./206_reverse_linked_list.md) — 🟢 Easy · the in-place reversal used in step 2
- [876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list) — 🟢 Easy · fast/slow pointer to find the middle
- [125. Valid Palindrome](./125_valid_palindrome.md) — 🟢 Easy · palindrome check with two pointers on a string
- [143. Reorder List](https://leetcode.com/problems/reorder-list) — 🟡 Medium · same find-middle + reverse-half technique
