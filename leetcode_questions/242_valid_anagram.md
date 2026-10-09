# 242. Valid Anagram

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/valid-anagram/)

## Question Description
Given two strings s and t, return true if t is an anagram of s, and false otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Example 1:

> Input: s = "anagram", t = "nagaram"
>
> Output: true

Example 2:

> Input: s = "rat", t = "car"
>
> Output: false
 

Constraints:

* 1 <= s.length, t.length <= 5 * 104
* s and t consist of lowercase English letters.

## Tags
- string
- hashMap

## Approach
**Key idea:** Two strings are anagrams exactly when they contain the same characters with the same counts.

1. If the lengths differ, return `False` immediately.
2. Count the characters of `s` and of `t`.
3. Return whether the two counts are equal.

## Code Implementation
```python
from collections import Counter

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        return Counter(s) == Counter(t)
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1) — at most 26 lowercase letters

## Related Problems
- [49. Group Anagrams](./49_group_anagrams.md) — 🟡 Medium · group strings by their character counts
- [438. Find All Anagrams in a String](./438_find_all_anagrams_in_a_string.md) — 🟡 Medium · compare counts over a sliding window
- [383. Ransom Note](https://leetcode.com/problems/ransom-note) — 🟢 Easy · character-count containment check
