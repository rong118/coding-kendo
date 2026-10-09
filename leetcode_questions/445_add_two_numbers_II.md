# 445. Add Two Numbers II

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/add-two-numbers-ii/)

## Question Description
You are given two **non-empty** linked lists representing two non-negative integers. The **most significant digit comes first** and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example 1:

> Input: l1 = [7,2,4,3], l2 = [5,6,4]
>
> Output: [7,8,0,7]

Example 2:

> Input: l1 = [2,4,3], l2 = [5,6,4]
>
> Output: [8,0,7]

Example 3:

> Input: l1 = [0], l2 = [0]
>
> Output: [0]

Constraints:

* The number of nodes in each linked list is in the range [1, 100].
* 0 <= Node.val <= 9
* It is guaranteed that the list represents a number that does not have leading zeros.

## Tags
- linkedlist

## Approach
**Key idea:** Addition must start from the least significant digit, which sits at the tail; pushing the digits onto stacks lets us pop them in reverse, and prepending each result node builds the answer in the right order.

1. Push every digit of `l1` onto stack `s1` and every digit of `l2` onto stack `s2`.
2. While either stack is non-empty or there is a carry, pop available digits and add them to the carry.
3. Split the total into a new carry and a digit with `divmod(total, 10)`.
4. Create a node for the digit and prepend it to the result list.
5. Return the head of the result.

## Code Implementation
```python
from typing import Optional

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        # Push digits onto stacks so we can process from least significant
        s1, s2 = [], []
        while l1:
            s1.append(l1.val)
            l1 = l1.next
        while l2:
            s2.append(l2.val)
            l2 = l2.next

        carry = 0
        head = None

        # Build result from right to left
        while s1 or s2 or carry:
            total = carry
            if s1:
                total += s1.pop()
            if s2:
                total += s2.pop()
            carry, digit = divmod(total, 10)
            head = ListNode(digit, head)

        return head
```

## Time Complexity Analysis
> Time complexity  : O(m + n) — traverse both lists plus build result
>
> Space complexity : O(m + n) — stacks plus output list

## Related Problems
- [2. Add Two Numbers](./2_add_two_numbers.md) — 🟡 Medium · same addition with digits stored in reverse
- [206. Reverse Linked List](./206_reverse_linked_list.md) — 🟢 Easy · alternative: reverse the lists instead of using stacks
- [234. Palindrome Linked List](./234_palindrome_linked_list.md) — 🟢 Easy · processing a singly linked list from both ends
