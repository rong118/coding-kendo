# 242. Valid Anagram

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
