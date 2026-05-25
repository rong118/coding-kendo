# 438. Find All Anagrams in a String

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
