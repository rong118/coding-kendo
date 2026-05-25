# 409. Longest Palindrome

## Question link
(https://leetcode.com/problems/longest-palindrome/)

## Question Description
Given a string s which consists of lowercase or uppercase letters, return the length of the longest palindrome that can be built with those letters.

Letters are case sensitive, for example, "Aa" is not considered a palindrome here.

Example 1:

> Input: s = "abccccdd"
>
> Output: 7
>
> Explanation: One longest palindrome that can be built is "dccaccd", whose length is 7.

Example 2:

> Input: s = "a"
> 
> Output: 1
>
> Explanation: The longest palindrome that can be built is "a", whose length is 1.

Constraints:
* 1 <= s.length <= 2000
* s consists of lowercase and/or uppercase English letters only.

## Tags
- string
- hashMap

## Code Implementation
```python
from collections import Counter

class Solution:
    def longestPalindrome(self, s: str) -> int:
        ans = 0
        has_odd = False
        for count in Counter(s).values():
            ans += count // 2 * 2
            if count % 2 == 1:
                has_odd = True
        return ans + (1 if has_odd else 0)
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1) — at most 52 uppercase/lowercase letters
