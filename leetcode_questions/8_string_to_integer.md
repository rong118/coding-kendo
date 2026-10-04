# 8. String to Integer (atoi)

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/string-to-integer-atoi/)

## Question Description
Implement the myAtoi(string s) function, which converts a string to a 32-bit signed integer (similar to C/C++'s atoi function).

The algorithm for myAtoi(string s) is as follows:

Read in and ignore any leading whitespace.
Check if the next character (if not already at the end of the string) is '-' or '+'. Read this character in if it is either. This determines if the final result is negative or positive respectively. Assume the result is positive if neither is present.
Read in next the characters until the next non-digit character or the end of the input is reached. The rest of the string is ignored.

Convert these digits into an integer (i.e. "123" -> 123, "0032" -> 32). If no digits were read, then the integer is 0. Change the sign as necessary (from step 2).
If the integer is out of the 32-bit signed integer range [-231, 231 - 1], then clamp the integer so that it remains in the range. Specifically, integers less than -231 should be clamped to -231, and integers greater than 231 - 1 should be clamped to 231 - 1.
Return the integer as the final result.
Note:

Only the space character ' ' is considered a whitespace character.
Do not ignore any characters other than the leading whitespace or the rest of the string after the digits.
 
Example 1:

> Input: s = "42"
>
> Output: 42

Example 2:

> Input: s = "   -42"
>
> Output: -42

Example 3:

> Input: s = "4193 with words"
>
> Output: 4193
 
Constraints:
* 0 <= s.length <= 200
* s consists of English letters (lower-case and upper-case), digits (0-9), ' ', '+', '-', and '.'.

## Tags
- string

## Approach
**Key idea:** Parse the string left to right in the exact order the spec describes — whitespace, optional sign, digits — and clamp once at the end (Python ints don't overflow).

1. Strip leading spaces; if nothing is left, return `0`.
2. If the first character is `+` or `-`, record the sign and skip it.
3. Read consecutive digits, building `num = num * 10 + digit`; stop at the first non-digit.
4. Apply the sign and clamp the result into `[-2^31, 2^31 - 1]`.

## Code Implementation
```python
class Solution:
    def myAtoi(self, s: str) -> int:
        s = s.lstrip()
        if not s:
            return 0

        sign = 1
        i = 0
        if s[0] == '-' or s[0] == '+':
            sign = -1 if s[0] == '-' else 1
            i = 1

        num = 0
        while i < len(s) and s[i].isdigit():
            num = num * 10 + int(s[i])
            i += 1

        num *= sign
        INT_MIN, INT_MAX = -2**31, 2**31 - 1
        return max(INT_MIN, min(num, INT_MAX))
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1)

## Related Problems
- [7. Reverse Integer](https://leetcode.com/problems/reverse-integer) — 🟡 Medium · digit-by-digit building with 32-bit overflow handling
- [65. Valid Number](https://leetcode.com/problems/valid-number) — 🔴 Hard · stricter character-by-character numeric parsing
- [58. Length of Last Word](./58_length_of_last_word.md) — 🟢 Easy · scanning a string while skipping spaces
