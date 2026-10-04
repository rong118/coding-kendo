# 58. Length of Last Word

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/length-of-last-word/)

## Question Description
Given a string `s` consisting of words and spaces, return the length of the **last** word in the string.

A **word** is a maximal substring consisting of non-space characters only.

Example 1:

> Input: s = "Hello World"
>
> Output: 5
>
> Explanation: The last word is "World" with length 5.

Example 2:

> Input: s = "   fly me   to   the moon  "
>
> Output: 4
>
> Explanation: The last word is "moon" with length 4.

Example 3:

> Input: s = "luffy is still joyboy"
>
> Output: 6
>
> Explanation: The last word is "joyboy" with length 6.

Constraints:

* 1 <= s.length <= 10^4
* s consists of only English letters and spaces `' '`.
* There will be at least one word in s.

## Tags
- string

## Approach
**Key idea:** Only the end of the string matters, so scan backward: skip the trailing spaces, then count characters until the next space.

1. Start `i` at the last index of `s`.
2. Move `i` left while `s[i]` is a space.
3. Move `i` left while `s[i]` is not a space, counting each character.
4. Return the count.

## Code Implementation
```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        # Skip trailing spaces
        i = len(s) - 1
        while i >= 0 and s[i] == ' ':
            i -= 1

        # Count last word length
        length = 0
        while i >= 0 and s[i] != ' ':
            length += 1
            i -= 1

        return length
```

## Time Complexity Analysis
> Time complexity  : O(n) — single pass from the end, where n is the length of s
>
> Space complexity : O(1) — only a counter variable

## Related Problems
- [151. Reverse Words in a String](./151_reverse_words_in_a_string.md) — 🟡 Medium · word parsing around extra spaces
- [14. Longest Common Prefix](./14_longest_common_prefix.md) — 🟢 Easy · simple character-by-character string scan
- [344. Reverse String](./344_reverse_string.md) — 🟢 Easy · basic in-place string traversal
