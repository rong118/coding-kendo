# 14. Longest Common Prefix

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/longest-common-prefix/)

## Question Description
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

Example 1:

> Input: strs = ["flower","flow","flight"]
>
> Output: "fl"

Example 2:

> Input: strs = ["dog","racecar","car"]
>
> Output: ""
>
> Explanation: There is no common prefix among the input strings.

Constraints:

* 1 <= strs.length <= 200
* 0 <= strs[i].length <= 200
* strs[i] consists of only lowercase English letters if it is non-empty.

## Tags
- string

## Approach
**Key idea:** The common prefix can be no longer than the shortest string, so scan that string column by column and stop at the first column where any string disagrees.

1. Pick the shortest string as the reference prefix.
2. For each index `i` and character `ch` of the reference, compare `s[i]` for every string `s`.
3. On the first mismatch, return `prefix[:i]`.
4. If no mismatch occurs, the whole reference string is the answer.

## Code Implementation
```python
class Solution:
    def longestCommonPrefix(self, strs: list[str]) -> str:
        if not strs:
            return ""

        # Use the shortest string as the reference
        prefix = min(strs, key=len)

        for i, ch in enumerate(prefix):
            for s in strs:
                if s[i] != ch:
                    return prefix[:i]

        return prefix
```

## Time Complexity Analysis
> Time complexity  : O(n * m) — where n is the number of strings and m is the length of the shortest string
>
> Space complexity : O(1) — only the result string is stored

## Related Problems
- [208. Implement Trie (Prefix Tree)](./208_implement_trie.md) — 🟡 Medium · prefixes stored and queried in a trie
- [28. Find the Index of the First Occurrence in a String](./28_find_the_index_of_the_first_occurrence_in_a_string.md) — 🟢 Easy · character-by-character string comparison
