# 14. Longest Common Prefix

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
