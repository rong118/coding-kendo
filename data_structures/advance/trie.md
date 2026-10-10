## Trie (Prefix Tree)

A Trie (also known as a prefix tree) is a type of search tree used to store a dynamic set or associative array where the keys are usually strings.

## key Characteristic
- Each node in the trie represents a string.
- The root node represents the empty string.
- Each edge from a node to its child represents appending one character to the string represented by that node.
- A node is said to be complete if all possible characters are present at each position in the string represented by that node.

## Implementation
### python Implementation
```python
class Trie:
    class Node:
        def __init__(self):
            self.is_end_of_word = False
            self.children = {}

    def __init__(self):
        self.root = self.Node()

    def insert(self, word):
        current = self.root
        for c in word:
            if c not in current.children:
                current.children[c] = self.Node()
            current = current.children[c]
        current.is_end_of_word = True

    def search(self, word):
        current = self.root
        for c in word:
            if c not in current.children:
                return False
            current = current.children[c]
        return current.is_end_of_word

    def prefix_search(self, prefix):
        current = self.root
        for c in prefix:
            if c not in current.children:
                return []  # prefix not found
            current = current.children[c]
        
        results = []
        self._search(current, prefix, results)
        return results

    def _search(self, node, prefix, results):
        if node.is_end_of_word:
            results.append(prefix)
        for c, child in node.children.items():
            self._search(child, prefix + c, results)

# Example usage
trie = Trie()

trie.insert("apple")
trie.insert("banana")
trie.insert("app")

print(f"Is 'apple' in the trie? {'Yes' if trie.search('apple') else 'No'}")
print(f"Is 'bananas' in the trie? {'Yes' if trie.search('bananas') else 'No'}")
print(f"Is 'apples' in the trie? {'Yes' if trie.search('apples') else 'No'}")

results = trie.prefix_search("a")  # returns ["apple", "app"]
for result in results:
    print(result)
```

## Runtime Complexity
### - Insertion

**O(m)**, where m is the length of the string. This is because we need to traverse the Trie, creating new nodes as needed, and update the child pointers. Each step takes constant time, so the total time complexity is linear in the length of the string.

### - Search

**O(m)**, where m is the length of the string. This is because we need to traverse the Trie, following the child pointers until we reach the end of the string. If the string is not found, the search operation will terminate earlier.

### - Prefix matching

The time complexity for finding all strings that start with a given prefix in a Trie is **O(n)**, where n is the number of strings in the Trie that match the prefix.

This is because we need to traverse the Trie, starting from the root node and following the child pointers until we reach the end of the string. We then need to collect all the strings that match the prefix.

## Leetcode questions

| # | Problem | Difficulty |
|---|---------|------------|
| 208 | [Implement Trie (Prefix Tree)](../../leetcode_questions/208_implement_trie.md) | Medium |
| 211 | [Design Add and Search Words Data Structure](../../leetcode_questions/211_design_add_search_words_data_structure.md) | Medium |
| 212 | [Word Search II](../../leetcode_questions/212_word_search_II.md) | Hard |
| 421 | [Maximum XOR of Two Numbers in an Array](../../leetcode_questions/421_maximum_xor_of_numbers_in_an_array.md) | Medium |
| 1707 | [Maximum XOR With an Element From Array](../../leetcode_questions/1707_maximum_xor_with_an_element_from_array.md) | Hard |
