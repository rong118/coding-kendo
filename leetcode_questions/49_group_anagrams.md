# 49. Group Anagrams

## Question link
(https://leetcode.com/problems/group-anagrams/)

## Question Description
Given an array of strings `strs`, group the **anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Example 1:

> Input: strs = ["eat","tea","tan","ate","nat","bat"]
>
> Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

Example 2:

> Input: strs = [""]
>
> Output: [[""]]

Example 3:

> Input: strs = ["a"]
>
> Output: [["a"]]

Constraints:

* 1 <= strs.length <= 10^4
* 0 <= strs[i].length <= 100
* strs[i] consists of lowercase English letters.

## Tags
- hashmap
- string

## Code Implementation
```python
from collections import defaultdict

class Solution:
    def groupAnagrams(self, strs: list[str]) -> list[list[str]]:
        groups = defaultdict(list)

        for s in strs:
            # Sort each string to produce a canonical key.
            # All anagrams share the same sorted string.
            key = ''.join(sorted(s))
            groups[key].append(s)

        return list(groups.values())
```

## Time Complexity Analysis
> Time complexity  : O(n * k log k) — where n is the number of strings and k is the maximum string length
>
> Space complexity : O(n * k) — the hash map stores all strings
