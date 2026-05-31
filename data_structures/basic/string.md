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

| # | Problem | Difficulty | Technique |
|---|---------|------------|-----------|
| 14 | [Longest Common Prefix](../../leetcode_questions/14_longest_common_prefix.md) | Easy | Horizontal character scan |
| 28 | [Find the Index of the First Occurrence in a String](../../leetcode_questions/28_find_the_index_of_the_first_occurrence_in_a_string.md) | Easy | Substring search |
| 58 | [Length of Last Word](../../leetcode_questions/58_length_of_last_word.md) | Easy | Reverse string traversal |
| 151 | [Reverse Words in a String](../../leetcode_questions/151_reverse_words_in_a_string.md) | Medium | Split, reverse, join |
| 344 | [Reverse String](../../leetcode_questions/344_reverse_string.md) | Easy | Two-pointer in-place swap |
