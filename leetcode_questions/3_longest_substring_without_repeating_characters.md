# 3. Longest Substring Without Repeating Characters

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/longest-substring-without-repeating-characters/)

## Question Description
Given a string s, find the length of the longest substring without repeating characters.

Example 1:

> Input: s = "abcabcbb"
>
> Output: 3
>
> Explanation: The answer is "abc", with the length of 3.

Example 2:

> Input: s = "bbbbb"
>
> Output: 1
>
> Explanation: The answer is "b", with the length of 1.

Example 3:

> Input: s = "pwwkew"
>
> Output: 3
>
> Explanation: The answer is "wke", with the length of 3.
>
> Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
 

Constraints:
- 0 <= s.length <= 5 * 10^4
- s consists of English letters, digits, symbols and spaces.

## Tags
- string
- sliding window
- hashMap

## Approach
**Key idea:** Keep a sliding window `[l, r]` that never contains a duplicate; when `s[r]` is already inside, shrink from the left until it is gone. Each character enters and leaves the window at most once.

1. Keep a set `seen` of the characters currently in the window and a left pointer `l = 0`.
2. Move `r` across the string one character at a time.
3. While `s[r]` is already in `seen`, remove `s[l]` from the set and advance `l`.
4. Add `s[r]` to the set; the window is now duplicate-free, so update the answer with `r - l + 1`.

## Code Implementation
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        seen = set()
        l = 0
        ans = 0

        for r in range(len(s)):
            while s[r] in seen:
                seen.remove(s[l])
                l += 1
            seen.add(s[r])
            ans = max(ans, r - l + 1)

        return ans
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1) — at most 128 ASCII characters in the set

## Related Problems
- [76. Minimum Window Substring](./76_minimum_window_substring.md) — 🔴 Hard · variable-size sliding window with a character count
- [438. Find All Anagrams in a String](./438_find_all_anagrams_in_a_string.md) — 🟡 Medium · sliding window over a string
- [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement) — 🟡 Medium · longest valid window, shrink when invalid
