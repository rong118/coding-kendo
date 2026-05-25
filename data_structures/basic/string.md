# String

A string is an immutable sequence of characters. In Python, strings support indexing, slicing, and a rich set of built-in methods.

## Complexity

| Operation | Time |
|---|---|
| Index / Slice | O(1) / O(k) |
| Search (in, find) | O(n) |
| Concatenation | O(n + m) |
| Split / Join | O(n) |

## Python Usage

```python
# Slicing
text = "PythonProgramming"
text[:6]     # "Python"
text[-11:]   # "Programming"

# Case
"hello".upper(); "HELLO".lower()

# Find & Replace
"hello".find("ll")                       # 2
"hello".replace("ll", "rr")             # "herro"

# Split & Join
"a,b,c".split(",")                      # ['a', 'b', 'c']
"-".join(['a', 'b', 'c'])               # "a-b-c"

# Substring checks
"Python" in "Hello, Python!"            # True
"banana".count("an")                     # 2

# Formatting
f"My name is {name} and I am {age} years old."
```

## Related LeetCode Questions

- [3. Longest Substring Without Repeating Characters](../../leetcode_questions/3_longest_substring_without_repeating_characters.md)
- [5. Longest Palindromic Substring](../../leetcode_questions/5_longest_palindromic_substring.md)
- [8. String to Integer](../../leetcode_questions/8_string_to_integer.md)
- [76. Minimum Window Substring](../../leetcode_questions/76_minimum_window_substring.md)
- [125. Valid Palindrome](../../leetcode_questions/125_valid_palindrome.md)
- [242. Valid Anagram](../../leetcode_questions/242_valid_anagram.md)
- [409. Longest Palindrome](../../leetcode_questions/409_longest_palindrome.md)
- [438. Find All Anagrams in a String](../../leetcode_questions/438_find_all_anagrams_in_a_string.md)
