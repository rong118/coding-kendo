# 438. Find All Anagrams in a String

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/find-all-anagrams-in-a-string/)

## Question Description
Given two strings s and p, return an array of all the start indices of p's anagrams in s. You may return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Example 1:

> Input: s = "cbaebabacd", p = "abc"
> 
> Output: [0,6]
>
> Explanation:
>
> The substring with start index = 0 is "cba", which is an anagram of "abc".
>
> The substring with start index = 6 is "bac", which is an anagram of "abc".

Example 2:

> Input: s = "abab", p = "ab"
>
> Output: [0,1,2]
>
> Explanation:
> The substring with start index = 0 is "ab", which is an anagram of "ab".
>
> The substring with start index = 1 is "ba", which is an anagram of "ab".
>
> The substring with start index = 2 is "ab", which is an anagram of "ab".
 

Constraints:
* 1 <= s.length, p.length <= 3 * 10^4
* s and p consist of lowercase English letters.

## Tags
- string
- hashMap

## Approach
**Key idea:** Two strings are anagrams exactly when their letter counts match, so slide a fixed-size window of length `len(p)` over `s` and compare its counts with `p`'s.

1. Count the letters of `p`.
2. Move a right edge across `s`, adding each new character to the window count.
3. Once the window is longer than `len(p)`, remove the character that falls off the left (deleting zero counts so the comparison stays exact).
4. Whenever the window count equals `p`'s count, record the window's start index `i - len(p) + 1`.

## Code Implementation
```python
from collections import Counter

class Solution:
    def findAnagrams(self, s: str, p: str) -> list[int]:
        p_count = Counter(p)
        window = Counter()
        ans = []

        for i in range(len(s)):
            window[s[i]] += 1
            if i >= len(p):
                if window[s[i - len(p)]] == 1:
                    del window[s[i - len(p)]]
                else:
                    window[s[i - len(p)]] -= 1
            if window == p_count:
                ans.append(i - len(p) + 1)

        return ans
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1) — at most 26 lowercase letters

## Related Problems
- [567. Permutation in String](https://leetcode.com/problems/permutation-in-string) — 🟡 Medium · same fixed-size window, boolean answer
- [76. Minimum Window Substring](./76_minimum_window_substring.md) — 🔴 Hard · variable-size window with count matching
- [242. Valid Anagram](./242_valid_anagram.md) — 🟢 Easy · anagram check via letter counts
- [49. Group Anagrams](./49_group_anagrams.md) — 🟡 Medium · grouping strings by letter counts
