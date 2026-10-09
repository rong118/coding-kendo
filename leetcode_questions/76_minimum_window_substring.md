# 76. Minimum Window Substring

**Difficulty:** 🔴 Hard

## Question link
(https://leetcode.com/problems/minimum-window-substring/)

## Question Description
Given two strings s and t of lengths m and n respectively, return the minimum window 
substring of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".

The testcases will be generated such that the answer is unique.

Example 1:

> Input: s = "ADOBECODEBANC", t = "ABC"
> 
> Output: "BANC"
>
> Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

Example 2:

> Input: s = "a", t = "a"
>
> Output: "a"
>
> Explanation: The entire string s is the minimum window.

Example 3:

> Input: s = "a", t = "aa"
>
> Output: ""
>
> Explanation: Both 'a's from t must be included in the window.
>
> Since the largest window of s only has one 'a', return empty string.
 

Constraints:
* m == s.length
* n == t.length
* 1 <= m, n <= 10^5
* s and t consist of uppercase and lowercase English letters.


## Tags
- string
- sliding window

## Approach
**Key idea:** Expand the right edge until the window covers all of `t`, then shrink the left edge as far as possible while it still covers `t`; every minimal valid window is seen this way.

1. Count the characters needed from `t` in `need`, and track `missing = len(t)` still uncovered.
2. Move `r` across `s`: if `s[r]` is still needed, decrement `missing`; always decrement `need[s[r]]`.
3. While `missing == 0`, record the window if it is the shortest so far.
4. Then drop `s[l]`: increment `need[s[l]]`, and if it becomes positive the window is no longer valid, so increment `missing`. Advance `l`.
5. Return the best window, or `""` if none was found.

## Code Implementation
```python
from collections import Counter

class Solution:
    def minWindow(self, s: str, t: str) -> str:
        need = Counter(t)
        missing = len(t)
        l = 0
        start, end = 0, float('inf')

        for r in range(len(s)):
            if need[s[r]] > 0:
                missing -= 1
            need[s[r]] -= 1

            while missing == 0:
                if r - l < end - start:
                    start, end = l, r
                if need[s[l]] >= 0:
                    missing += 1
                need[s[l]] += 1
                l += 1

        return s[start:end + 1] if end != float('inf') else ""
```

## Time Complexity Analysis
> Time complexity  : O(m + n) — each index of s enters and leaves the window at most once, plus counting t
>
> Space complexity : O(1) — at most 52 uppercase/lowercase letters

## Related Problems
- [3. Longest Substring Without Repeating Characters](./3_longest_substring_without_repeating_characters.md) — 🟡 Medium · variable-size sliding window
- [438. Find All Anagrams in a String](./438_find_all_anagrams_in_a_string.md) — 🟡 Medium · sliding window with character counts
- [567. Permutation in String](https://leetcode.com/problems/permutation-in-string) — 🟡 Medium · window must cover a target's character counts
- [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum) — 🔴 Hard · sliding window
