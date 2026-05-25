# 5. Longest Palindromic Substring

## Question link
(https://leetcode.com/problems/longest-palindromic-substring/)

## Question Description
Given a string s, return the longest palindromic substring in s.

Example 1:

> Input: s = "babad"
>
> Output: "bab"
>
> Explanation: "aba" is also a valid answer.

Example 2:

> Input: s = "cbbd"
>
> Output: "bb"

Constraints:
* 1 <= s.length <= 1000
* s consist of only digits and English letters.

## Tags
- string
- dynamic programming

## Code Implementation
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        def expand(l: int, r: int) -> str:
            while l >= 0 and r < len(s) and s[l] == s[r]:
                l -= 1
                r += 1
            return s[l + 1:r]

        res = ""
        for i in range(len(s)):
            odd = expand(i, i)
            even = expand(i, i + 1)
            if len(odd) > len(res):
                res = odd
            if len(even) > len(res):
                res = even

        return res
```

## Time Complexity Analysis
> Time complexity  : O(n^2)
>
> Space complexity : O(1)
