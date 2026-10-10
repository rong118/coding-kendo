# Union-Find (Disjoint-Set)

The Union-Find, also known as the Disjoint-Set, is a tree-like data structure used for handling the union and find operations on disjoint sets. 

It determines whether several elements are in the same group.

## Key characteristics

A Union-Find data structure represents a set of elements, where each element belongs to one or more groups (sets). The primary operations are:

- **MakeSet**: Create a new set containing a given element.
- **Find**: Determines which subset a particular element is in. This can be used to determine if two elements are in the same subset.
- **Union**: Joins two subsets into a single subset.

## Implmentation
```python
class DSU:
    def __init__(self, N):
        # Initialize the parent list where each node is its own parent
        self.parent = list(range(N))

    def _find(self, x):
        # Path compression: Make the parent of x point directly to the root
        if self.parent[x] != x:
            self.parent[x] = self._find(self.parent[x])
        return self.parent[x]

    def _union(self, x, y):
        # Union by making the root of one tree point to the root of another
        self.parent[self._find(x)] = self._find(y)

if __name__ == "__main__":
    dsu = DSU(5)  # Create a DSU with 5 elements (0 to 4)

    # Union some sets
    dsu._union(0, 1)
    dsu._union(1, 2)

    # Find roots
    print(dsu._find(0))  # Should output the root of the set containing 0
    print(dsu._find(2))  # Should output the same root as 0's set
    print(dsu._find(3))  # Should output 3, as it is its own root

    # Check if two elements are in the same set
    print(dsu._find(0) == dsu._find(2))  # True
    print(dsu._find(0) == dsu._find(3))  # False
```

## Optimize Implementation

The most efficient implementation uses two techniques: 
- **Path Compression**
- **Union by Rank/Size**

### Union by Size Example
```python
class DSU:
    def __init__(self, N):
        # Initialize parent and size arrays
        self.parent = list(range(N))  # Each element is initially its own parent
        self.size = [1] * N  # Size of each set is initially 1

    def _find(self, x):
        # Path compression: Make the parent of x point directly to the root
        if self.parent[x] != x:
            self.parent[x] = self._find(self.parent[x])
        return self.parent[x]

    def _union(self, x, y):
        # Find the roots of the sets containing x and y
        rootx = self._find(x)
        rooty = self._find(y)

        if rootx != rooty:
            # Union by size: attach smaller tree under the larger tree
            if self.size[rootx] <= self.size[rooty]:
                self.parent[rootx] = rooty
                self.size[rooty] += self.size[rootx]
            else:
                self.parent[rooty] = rootx
                self.size[rootx] += self.size[rooty]

```

## Runtime Complexity

The runtime complexity of these operations depends on the implementation of the data structure. The most efficient implementation uses two techniques: **path compression** and **union by rank/size**.

### Techniques

- Path Compression:
  This technique flattens the structure of the tree whenever find is called, by making each node point directly to the root. This drastically reduces the time complexity of future operations.
- Union by Rank/Size:
  This technique ensures that the smaller tree (rank/size) is always added under the root of the larger tree (rank/size). This keeps the tree as flat as possible.

### Complexity

When both path compression and union by rank/size are used, the amortized time complexity for both the find and union operations is nearly constant. Specifically, the time complexity is:

- Find operation: **O(α(n))**
- Union operation: **O(α(n))**

α(n) is the inverse Ackermann function, which grows extremely slowly. For all practical purposes, α(n) can be considered a constant.

## Leetcode Questions

| # | Problem | Difficulty |
|---|---------|------------|
| 305 | [Number of Islands II](../../leetcode_questions/305_number_of_island_ii.md) | Hard |
| 547 | [Number of Provinces](../../leetcode_questions/547_number_of_provinces.md) | Medium |
| 128 | [Longest Consecutive Sequence](../../leetcode_questions/128_longest_consecutive_sequence.md) | Medium |
| 261 | [Graph Valid Tree](../../leetcode_questions/261_graph_valid_tree.md) | Medium |
