# String

In computer science, a **string** is a sequence of characters used to represent text. It's a core data type in most programming languages.

## Python Examples
```python
# 1. Concatenation
str1, str2 = "Hello", "World"
print(str1 + " " + str2)  # Hello World

# 2. Slicing
text = "PythonProgramming"
print(text[:6])     # Python
print(text[-11:])   # Programming

# 3. Case Conversion
text = "hello, World!"
print(text.upper())      # HELLO, WORLD!
print(text.lower())      # hello, world!
print(text.capitalize()) # Hello, world!

# 4. Find & Replace
text = "I love programming in Python."
print(text.find("Python"))                     # 23
print(text.replace("Python", "JavaScript"))    # I love programming in JavaScript.

# 5. Split & Join
text = "apple,banana,cherry"
fruits = text.split(",")
print(fruits)                   # ['apple', 'banana', 'cherry']
print("-".join(fruits))         # apple-banana-cherry

# 6. Content Checks
text = "Python123"
print(text.isalpha())  # False
print(text.isalnum())  # True
print(text.isdigit())  # False

# 7. String Formatting
name, age = "Alice", 25
print(f"My name is {name} and I am {age} years old.")
# My name is Alice and I am 25 years old.

# 8, substring
text = "Hello, Python!"

# Check if a substring exists
print("Python" in text)     # True
print("Java" in text)       # False

# Count occurrences of a substring
text = "banana"
print(text.count("an"))     # 2
```

## Leetcode Questions
- [3. Longest Substring Without Repeating Characters](../../leetcode_questions/3_longest_substring_without_repeating_characters.md)
- [5. Longest Palindromic Substring](../../leetcode_questions/5_longest_palindromic_substring.md)
- [8. String to Integer](../../leetcode_questions/8_string_to_integer.md)
- [76. Minimum Window Substring](../../leetcode_questions/76_minimum_window_substring.md)
- [125. Valid Palindrome](../../leetcode_questions/125_valid_palindrome.md)
- [242. Valid Anagram](../../leetcode_questions/242_valid_anagram.md)
- [409. Longest Palindrome](../../leetcode_questions/409_longest_palindrome.md)
- [438. Find All Anagrams in a String](../../leetcode_questions/438_find_all_anagrams_in_a_string.md)