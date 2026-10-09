# 211. Design Add and Search Words Data Structure

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/design-add-and-search-words-data-structure/)

## Question Description
Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the WordDictionary class:
- WordDictionary() Initializes the object.
- void addWord(word) Adds word to the data structure, it can be matched later.
- bool search(word) Returns true if there is any string in the data structure that matches word or false otherwise. word may contain dots '.' where dots can be matched with any letter.

Example
> Input:
>
> ["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
> [[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
>
> Output:
>
> [null,null,null,null,false,true,true,true]
>
> Explanation:
> WordDictionary wordDictionary = new WordDictionary();
> wordDictionary.addWord("bad");
> wordDictionary.addWord("dad");
> wordDictionary.addWord("mad");
> wordDictionary.search("pad"); // return False
> wordDictionary.search("bad"); // return True
> wordDictionary.search(".ad"); // return True
> wordDictionary.search("b.."); // return True

Constraints:
- 1 <= word.length <= 500
- word in addWord consists lower-case English letters.
- word in search consist of  '.' or lower-case English letters.
- At most 50000 calls will be made to addWord and search.

## Tags
- Trie
- DFS
- backtracking

## Approach
**Key idea:** Store the words in a trie. A normal letter follows one child; a `.` tries every child with DFS, and the search succeeds if any branch reaches the end of a word.

1. Each trie node has a `children` map and an `is_word` flag.
2. `addWord`: walk down from the root, creating missing children, and mark the last node with `is_word = True`.
3. `search`: run `dfs(pos, node)`; when `pos` reaches the end of the word, return `node.is_word`.
4. If `word[pos]` is a letter, continue into that child (fail if it is missing).
5. If it is `.`, try `dfs(pos + 1, child)` for every child and return `True` as soon as one matches.

## Code Implementation
```python
class TrieNode:
    def __init__(self):
        self.children: dict[str, "TrieNode"] = {}
        self.is_word = False

class WordDictionary:
    def __init__(self):
        self.root = TrieNode()

    def addWord(self, word: str) -> None:
        node = self.root
        for ch in word:
            node = node.children.setdefault(ch, TrieNode())
        node.is_word = True

    def search(self, word: str) -> bool:
        def dfs(pos: int, node: TrieNode) -> bool:
            if pos == len(word):
                return node.is_word
            ch = word[pos]
            if ch == '.':
                return any(dfs(pos + 1, child) for child in node.children.values())
            child = node.children.get(ch)
            return child is not None and dfs(pos + 1, child)

        return dfs(0, self.root)
```

## Time Complexity Analysis
> Time complexity  : addWord O(L); search O(L) without dots, O(N) worst case with dots — L = word length, N = trie nodes
>
> Space complexity : O(N) — total characters stored in the trie, plus O(L) recursion stack

## Related Problems
- [208. Implement Trie (Prefix Tree)](./208_implement_trie.md) — 🟡 Medium · the basic trie insert and search
- [212. Word Search II](./212_word_search_II.md) — 🔴 Hard · trie plus DFS backtracking
- [421. Maximum XOR of Two Numbers in an Array](./421_maximum_xor_of_numbers_in_an_array.md) — 🟡 Medium · searching a trie branch by branch
