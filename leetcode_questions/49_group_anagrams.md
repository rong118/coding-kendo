# 49. Group Anagrams

**Difficulty:** 🟡 Medium

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

## Approach
**Key idea:** Anagrams contain exactly the same letters, so sorting a word produces a canonical key that all of its anagrams share.

1. Create a hash map from key to a list of words.
2. For each string, sort its characters to build the key.
3. Append the original string to the list for that key.
4. Return all lists in the map.

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

## Related Problems
- [242. Valid Anagram](./242_valid_anagram.md) — 🟢 Easy · checks whether two strings are anagrams
- [438. Find All Anagrams in a String](./438_find_all_anagrams_in_a_string.md) — 🟡 Medium · anagram matching with a sliding window
- [249. Group Shifted Strings](https://leetcode.com/problems/group-shifted-strings) — 🟡 Medium · group strings by a canonical key
