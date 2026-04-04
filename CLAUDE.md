# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

**Coding Kendo** is a knowledge base for data structures, algorithms, complexity analysis, and LeetCode interview questions. All content is written in Markdown with Python code examples.

## Content Structure

```
data_structures/
  basic/        # Array, String, Linked List, Stack, Queue, Heap, Hashing, TreeMap
  tree/         # Tree, Binary Tree/BST, AVL, B-Tree, tree search, traversal
  graph/        # Graph, BFS/DFS, topological sort, shortest path, MST
  advance/      # Trie, Union Find, Binary Index Tree, Segment Tree
algorithms/
  basic/        # Sort (bubble, selection, merge, quick), Search (linear, binary)
  others/       # Brute force, backtracking, recursion, divide & conquer, two pointers,
                #   sliding window, greedy, dynamic programming, math
  BigONotation.md
  CommonRuntime.md
leetcode_questions/   # One file per problem: {id}_{slug}.md
resources/assets/     # Images referenced in docs (currently deleted from working tree)
```

## Document Conventions

Each **data structure / algorithm** file follows this pattern:
1. Concept explanation
2. Python implementation example
3. Runtime complexity analysis
4. Linked LeetCode questions

Each **LeetCode question** file follows this pattern:
1. Question link (LeetCode URL)
2. Question description with examples and constraints
3. `## Tags` listing relevant topics
4. `## Code Implementation` — Python solution
5. `## Time Complexity Analysis` — Big-O for time and space

## Adding New Content

- New LeetCode problem: create `leetcode_questions/{id}_{slug}.md` following the pattern above.
- New topic: create the `.md` file in the appropriate subdirectory and add a link to `README.md`.
- Code examples must be in Python.
- Link back from the data structure/algorithm page to any related LeetCode questions.
