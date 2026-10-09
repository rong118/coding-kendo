# 208. Implement Trie

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/implement-trie-prefix-tree/)

## Question Description
A trie (pronounced as "try") or prefix tree is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:
- Trie() Initializes the trie object.
- void insert(String word) Inserts the string word into the trie.
- boolean search(String word) Returns true if the string word is in the trie (i.e., was inserted before), and false otherwise.
- boolean startsWith(String prefix) Returns true if there is a previously inserted string word that has the prefix prefix, and false otherwise.

Example:

> Input:
> ["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
> [[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
>
> Output:
> [null, null, true, false, true, null, true]
>
> Explanation:
>
> Trie trie = new Trie();
> trie.insert("apple");
> trie.search("apple");   // return True
> trie.search("app");     // return False
> trie.startsWith("app"); // return True
> trie.insert("app");
> trie.search("app");     // return True

Constraints:
- 1 <= word.length, prefix.length <= 2000
- word and prefix consist only of lowercase English letters.
- At most 3 * 10<sup>4</sup> calls in total will be made to insert, search, and startsWith.

## Tags
- Trie

## Approach
**Key idea:** Each node represents a prefix and holds one child per next letter, so a word or prefix is found by walking one node per character; a flag marks nodes where a complete word ends.

1. Each `TrieNode` has `children` (letter → node) and an `is_word` flag; the trie starts with an empty root.
2. `insert(word)`: walk from the root, creating missing child nodes, then set `is_word = True` on the last node.
3. `search(word)`: walk the characters; return `False` if a child is missing, otherwise return the last node's `is_word`.
4. `startsWith(prefix)`: same walk, but return `True` as soon as every character is matched.

## Code Implementation
```python
from typing import Optional


class TrieNode:
    def __init__(self):
        self.children: dict[str, "TrieNode"] = {}
        self.is_word = False


class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        node = self.root
        for c in word:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
        node.is_word = True

    def _walk(self, s: str) -> Optional[TrieNode]:
        node = self.root
        for c in s:
            if c not in node.children:
                return None
            node = node.children[c]
        return node

    def search(self, word: str) -> bool:
        node = self._walk(word)
        return node is not None and node.is_word

    def startsWith(self, prefix: str) -> bool:
        return self._walk(prefix) is not None
```

## Time Complexity Analysis
Input word length is n.
- insert()  => O(n)
- search()  => O(n)
- startsWith() => O(n)

> Time complexity  : O(n) per operation, where n is the length of the word/prefix
>
> Space complexity : O(total characters inserted) — at most one new node per inserted character

## Related Problems
- [211. Design Add and Search Words Data Structure](./211_design_add_search_words_data_structure.md) — 🟡 Medium · trie with wildcard search
- [212. Word Search II](./212_word_search_II.md) — 🔴 Hard · trie used to prune a board DFS
- [421. Maximum XOR of Two Numbers in an Array](./421_maximum_xor_of_numbers_in_an_array.md) — 🟡 Medium · bitwise trie over number bits
- [14. Longest Common Prefix](./14_longest_common_prefix.md) — 🟢 Easy · prefix matching across words
