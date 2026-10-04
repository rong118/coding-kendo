# 125. Valid Palindrome

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/valid-palindrome/)

## Question Description
A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

Example 1:

> Input: s = "A man, a plan, a canal: Panama"
> 
> Output: true
>
> Explanation: "amanaplanacanalpanama" is a palindrome.

Example 2:

> Input: s = "race a car"
>
> Output: false
>
> Explanation: "raceacar" is not a palindrome.

Example 3:

> Input: s = " "
>
> Output: true
> Explanation: s is an empty string "" after removing non-alphanumeric characters.
> Since an empty string reads the same forward and backward, it is a palindrome.
 

Constraints:

* 1 <= s.length <= 2 * 10^5
* s consists only of printable ASCII characters.

## Tags
- string

## Approach
**Key idea:** Compare characters from both ends inward, skipping anything that is not alphanumeric, so no cleaned copy of the string is needed.

1. Put `l` at the start and `r` at the end of `s`.
2. Advance `l` past non-alphanumeric characters, and move `r` back past them.
3. Compare `s[l].lower()` with `s[r].lower()`; if they differ, return `False`.
4. Move both pointers inward and repeat until they meet, then return `True`.

## Code Implementation
```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        l, r = 0, len(s) - 1
        while l < r:
            while l < r and not s[l].isalnum():
                l += 1
            while l < r and not s[r].isalnum():
                r -= 1
            if s[l].lower() != s[r].lower():
                return False
            l += 1
            r -= 1
        return True
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1)

## Related Problems
- [680. Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii) — 🟢 Easy · same two-pointer check allowing one deletion
- [234. Palindrome Linked List](./234_palindrome_linked_list.md) — 🟢 Easy · palindrome check on a linked list
- [344. Reverse String](./344_reverse_string.md) — 🟢 Easy · two pointers swapping from both ends
- [5. Longest Palindromic Substring](./5_longest_palindromic_substring.md) — 🟡 Medium · palindromes via expansion around centers
