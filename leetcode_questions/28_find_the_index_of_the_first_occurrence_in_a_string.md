# 28. Find the Index of the First Occurrence in a String

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
