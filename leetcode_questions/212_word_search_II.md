# 212. Word Search II

**Difficulty:** 🔴 Hard

## Question link
(https://leetcode.com/problems/word-search-ii/)

## Question Description
Given an m x n board of characters and a list of strings words, return all words on the board.

Each word must be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

> Example 1
>
>![Image](https://assets.leetcode.com/uploads/2020/11/07/search1.jpg)
>
> Input: board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]
>
> Output: ["eat","oath"]

> Example 2
>
>![Image](https://assets.leetcode.com/uploads/2020/11/07/search2.jpg)
>
> Input: board = [["a","b"],["c","d"]], words = ["abcb"]
>
> Output: []

Constraints:
- m == board.length
- n == board[i].length
- 1 <= m, n <= 12
- board[i][j] is a lowercase English letter.
- 1 <= words.length <= 3 * 10<sup>4</sup>
- 1 <= words[i].length <= 10
- words[i] consists of lowercase English letters.
- All the strings of words are unique.

## Tags
- dfs
- tire (用在空间优化)
- 从每一个位置暴力展开向4个方向，同时用Trie的searchPrefix来做减枝

## Approach
**Key idea:** Put all words in a trie and DFS from every cell, walking the trie alongside the board — as soon as the current path is not a prefix of any word, prune.

1. Insert every word into a trie; mark the end node with the word itself.
2. From each cell, start a DFS with the trie root.
3. At each step, move to the trie child for the cell's letter; if there is none, stop (prefix pruning).
4. If the trie node ends a word, record it and clear the mark so it is not reported twice.
5. Mark the cell as visited, recurse into the 4 neighbors, then restore the cell (backtrack).

## Code Implementation
```python
class TrieNode:
    def __init__(self):
        self.children: dict[str, "TrieNode"] = {}
        self.word: Optional[str] = None


class Solution:
    def findWords(self, board: list[list[str]], words: list[str]) -> list[str]:
        root = TrieNode()
        for w in words:
            node = root
            for c in w:
                node = node.children.setdefault(c, TrieNode())
            node.word = w

        m, n = len(board), len(board[0])
        found = []

        def dfs(x: int, y: int, parent: TrieNode) -> None:
            c = board[x][y]
            node = parent.children.get(c)
            if not node:
                return  # no word has this prefix — prune
            if node.word:
                found.append(node.word)
                node.word = None  # avoid duplicates
            board[x][y] = "#"  # mark visited
            for dx, dy in ((-1, 0), (1, 0), (0, -1), (0, 1)):
                nx, ny = x + dx, y + dy
                if 0 <= nx < m and 0 <= ny < n and board[nx][ny] != "#":
                    dfs(nx, ny, node)
            board[x][y] = c  # backtrack

        for i in range(m):
            for j in range(n):
                dfs(i, j, root)
        return found
```

## Time Complexity Analysis
> Time complexity  : O(M * N * 3^L) — L is the max word length (≤ 10); each DFS branches into at most 3 unvisited neighbors
>
> Space complexity : O(W * L) — trie over all W words, plus O(L) recursion depth

## Related Problems
- [79. Word Search](https://leetcode.com/problems/word-search) — 🟡 Medium · the single-word backtracking version
- [208. Implement Trie (Prefix Tree)](./208_implement_trie.md) — 🟡 Medium · the trie used for prefix pruning
- [211. Design Add and Search Words Data Structure](./211_design_add_search_words_data_structure.md) — 🟡 Medium · DFS through a trie
