# 344. Reverse String

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/reverse-string/)

## Question Description
Write a function that reverses a string. The input string is given as an array of characters `s`.

You must do this by modifying the input array **in-place** with O(1) extra memory.

Example 1:

> Input: s = ["h","e","l","l","o"]
>
> Output: ["o","l","l","e","h"]

Example 2:

> Input: s = ["H","a","n","n","a","h"]
>
> Output: ["h","a","n","n","a","H"]

Constraints:

* 1 <= s.length <= 10^5
* s[i] is a printable ascii character.

## Tags
- string
- two-pointers

## Approach
**Key idea:** Reversing is just swapping mirror positions, so two pointers walking inward from both ends finish it in place.

1. Set `l = 0` and `r = len(s) - 1`.
2. While `l < r`, swap `s[l]` and `s[r]`.
3. Move `l` right and `r` left.
4. Stop when the pointers meet; the middle element (if any) stays put.

## Code Implementation
```python
class Solution:
    def reverseString(self, s: list[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        l, r = 0, len(s) - 1
        while l < r:
            s[l], s[r] = s[r], s[l]
            l += 1
            r -= 1
```

## Time Complexity Analysis
> Time complexity  : O(n) — each character swapped once
>
> Space complexity : O(1) — in-place with two pointer variables

## Related Problems
- [125. Valid Palindrome](./125_valid_palindrome.md) — 🟢 Easy · two pointers from both ends
- [151. Reverse Words in a String](./151_reverse_words_in_a_string.md) — 🟡 Medium · string reversal applied to words
- [206. Reverse Linked List](./206_reverse_linked_list.md) — 🟢 Easy · reversal on a linked list
