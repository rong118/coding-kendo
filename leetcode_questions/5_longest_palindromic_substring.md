# 5. Longest Palindromic Substring

**Difficulty:** 🟡 Medium

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

## Approach
**Key idea:** Every palindrome mirrors around a center, and there are only `2n - 1` centers (each character and each gap between two characters), so expanding outward from each center finds every maximal palindrome.

1. For each index `i`, treat `i` as an odd-length center and `(i, i + 1)` as an even-length center.
2. Expand outward while both ends are in bounds and the characters match.
3. The substring between the last matching ends is the longest palindrome for that center.
4. Keep whichever palindrome found so far is longest.

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

## Related Problems
- [647. Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings) — 🟡 Medium · same expand-around-center counting
- [516. Longest Palindromic Subsequence](https://leetcode.com/problems/longest-palindromic-subsequence) — 🟡 Medium · palindrome DP over subsequences
- [409. Longest Palindrome](./409_longest_palindrome.md) — 🟢 Easy · building the longest palindrome from character counts
- [125. Valid Palindrome](./125_valid_palindrome.md) — 🟢 Easy · two-pointer palindrome check
