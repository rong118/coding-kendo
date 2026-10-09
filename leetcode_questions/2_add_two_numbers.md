# 2. Add Two Numbers

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/add-two-numbers/)

## Question Description
You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example 1:

> Input: l1 = [2,4,3], l2 = [5,6,4]
>
> Output: [7,0,8]
>
> Explanation: 342 + 465 = 807.

Example 2:

> Input: l1 = [0], l2 = [0]
>
> Output: [0]

Example 3:

> Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
>
> Output: [8,9,9,9,0,0,0,1]

Constraints:

* The number of nodes in each linked list is in the range [1, 100].
* 0 <= Node.val <= 9
* It is guaranteed that the list represents a number that does not have leading zeros.

## Tags
- linkedlist

## Approach
**Key idea:** The digits are stored least-significant first, so we can add the lists column by column like grade-school addition, carrying overflow into the next node.

1. Start with a dummy head node and `carry = 0`.
2. While either list still has nodes or `carry` is non-zero, add `carry` plus the current digit of each list.
3. Split the total with `divmod(total, 10)` into the new `carry` and the digit to append.
4. Advance both list pointers and return `dummy.next`.

## Code Implementation
```python
from typing import Optional

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = tail = ListNode(0)
        carry = 0

        while l1 or l2 or carry:
            total = carry
            if l1:
                total += l1.val
                l1 = l1.next
            if l2:
                total += l2.val
                l2 = l2.next

            carry, digit = divmod(total, 10)
            tail.next = ListNode(digit)
            tail = tail.next

        return dummy.next
```

## Time Complexity Analysis
> Time complexity  : O(max(m, n)) — single pass through the longer list
>
> Space complexity : O(max(m, n)) — output list length

## Related Problems
- [445. Add Two Numbers II](./445_add_two_numbers_II.md) — 🟡 Medium · same addition, but digits stored most-significant first
- [21. Merge Two Sorted Lists](./21_merge_two_sorted_lists.md) — 🟢 Easy · dummy-head technique for building a list
- [67. Add Binary](https://leetcode.com/problems/add-binary) — 🟢 Easy · digit-by-digit addition with carry
- [415. Add Strings](https://leetcode.com/problems/add-strings) — 🟢 Easy · digit-by-digit addition with carry
