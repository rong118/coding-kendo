# 269. Alien Dictionary

**Difficulty:** 🔴 Hard

## Question link
(https://leetcode.com/problems/alien-dictionary/)

## Question Description
There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of non-empty words from the dictionary, where words are sorted lexicographically by the rules of this new language. Derive the order of letters in this language.

<br/>

Example 1:
> Given the following words in dictionary,
>
> [
>  "wrt",
>  "wrf",
>  "er",
>  "ett",
>  "rftt"
> ]
>
> The correct order is: "wertf".

Example 2:
> Given the following words in dictionary,
>
> [
>  "z",
>  "x"
> ]
>
> The correct order is: "zx".

Example 3:
> Given the following words in dictionary,
>
> [
>  "z",
>  "x",
>  "z"
> ]
>
> The order is invalid, so return "".


Note:
- You may assume all letters are in lowercase.
- You may assume that if a is a prefix of b, then a must appear before b in the given dictionary.
- If the order is invalid, return an empty string.
- There may be multiple valid order of letters, return any one of them is fine.

<br/>

## Tags
- graph
- topologic sort

## Approach
**Key idea:** The first differing letter of two adjacent words gives one ordering rule `a < b`; collecting these rules as edges and topologically sorting them yields a valid alphabet, and a cycle means none exists.

1. Create a graph node (indegree 0) for every letter that appears.
2. For each adjacent pair of words, return `""` if the longer word comes first and the shorter is its prefix.
3. Otherwise find the first differing letters `a`, `b` and add edge `a -> b` (once), incrementing `b`'s indegree.
4. Run Kahn's BFS: repeatedly output a letter with indegree 0 and decrement its neighbours.
5. If not every letter was output, there is a cycle — return `""`.

## Code Implementation
```python
from collections import deque


class Solution:
    def alienOrder(self, words: list[str]) -> str:
        graph: dict[str, set[str]] = {c: set() for word in words for c in word}
        indegree = {c: 0 for c in graph}

        for w1, w2 in zip(words, words[1:]):
            # "abc" before "ab" is impossible in any ordering
            if len(w1) > len(w2) and w1.startswith(w2):
                return ""
            for a, b in zip(w1, w2):
                if a != b:
                    if b not in graph[a]:
                        graph[a].add(b)
                        indegree[b] += 1
                    break  # only the first difference carries information

        q = deque(c for c in indegree if indegree[c] == 0)
        order: list[str] = []
        while q:
            c = q.popleft()
            order.append(c)
            for nxt in graph[c]:
                indegree[nxt] -= 1
                if indegree[nxt] == 0:
                    q.append(nxt)

        # Letters left over are on a cycle -> contradictory order
        return "".join(order) if len(order) == len(indegree) else ""
```

## Time Complexity Analysis
> Time complexity  : O(C) — C is the total number of characters across all words
>
> Space complexity : O(1) — at most 26 letters and 26 × 26 edges

## Related Problems
- [207. Course Schedule](./207_course_schedule.md) — 🟡 Medium · topological sort / cycle detection
- [210. Course Schedule II](./210_course_schedule_ii.md) — 🟡 Medium · output a topological order
- [953. Verifying an Alien Dictionary](https://leetcode.com/problems/verifying-an-alien-dictionary) — 🟢 Easy · the reverse: order given, check the words
