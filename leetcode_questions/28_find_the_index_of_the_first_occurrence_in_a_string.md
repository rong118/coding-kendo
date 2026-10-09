# 28. Find the Index of the First Occurrence in a String

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)

## Question Description
Given two strings `needle` and `haystack`, return the index of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

Example 1:

> Input: haystack = "sadbutsad", needle = "sad"
>
> Output: 0
>
> Explanation: "sad" occurs at index 0 and 6. The first occurrence is at index 0, so we return 0.

Example 2:

> Input: haystack = "leetcode", needle = "leeto"
>
> Output: -1
>
> Explanation: "leeto" did not occur in "leetcode", so we return -1.

Constraints:

* 1 <= haystack.length, needle.length <= 10^4
* haystack and needle consist of only lowercase English characters.

## Tags
- string
- two-pointers

## Approach
**Key idea:** Slide a window of length `len(needle)` across `haystack` and return the first start position whose window equals `needle`.

1. Let `n = len(haystack)` and `m = len(needle)`.
2. For every start `i` from `0` to `n - m`, compare `haystack[i:i + m]` with `needle`.
3. Return `i` on the first match.
4. If no window matches, return `-1`.

## Code Implementation
```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        n, m = len(haystack), len(needle)

        for i in range(n - m + 1):
            if haystack[i:i + m] == needle:
                return i

        return -1
```

## Time Complexity Analysis
> Time complexity  : O(n * m) — worst case when many near-matches are checked; O(n + m) average with Python's fast substring slicing
>
> Space complexity : O(1) — no extra space used

## Related Problems
- [14. Longest Common Prefix](./14_longest_common_prefix.md) — 🟢 Easy · character-by-character string comparison
- [459. Repeated Substring Pattern](https://leetcode.com/problems/repeated-substring-pattern) — 🟢 Easy · substring search on a string
- [686. Repeated String Match](https://leetcode.com/problems/repeated-string-match) — 🟡 Medium · find a pattern inside a (repeated) text
- [214. Shortest Palindrome](https://leetcode.com/problems/shortest-palindrome) — 🔴 Hard · KMP-style prefix matching
