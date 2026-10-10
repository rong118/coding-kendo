# Tree Search

Searching a tree can be done using various algorithms, including Depth-First Search (DFS) and Breadth-First Search (BFS). 

Both DFS and BFS traverse the tree by visiting nodes in a specific order, but they differ in their approach.

## Depth-First Search (DFS)

- Start at an arbitrary node (called the "root" node).
- Visit the root node.
- Recursively visit each child of the current node until you reach a leaf node (a node with no children).
- Backtrack to the previous node and repeat the process until you return to the starting node.

### Example
```
  A
 / \
B   C
   /  \ 
   D   E
  /
  F
```
DFS would traverse this tree in the following order: A -> B -> C -> D-> F -> E

## Breadth-First Search (BFS)
- Start at an arbitrary node (called the "root" node).
- Visit all the child nodes of the root node.
- Then, visit all the grandchildren of the root node.
- Continue this process until you have visited all nodes in the tree.

### Example
```
  A
 / \
B   C
   /  \ 
   D   E
  /
  F
```
BFS would traverse this tree in the following order: A -> ( B -> C) -> (D-> E) -> F

## Key differences:
- DFS explores as far as possible along each branch before backtracking.
- BFS visits all nodes at a given level before moving on to the next level.

## Runtime Complexity
### Depth-First Search (DFS):
- Best-case scenario: O(n), where n is the number of nodes in the binary tree.
- Worst-case scenario: O(n), where n is the number of nodes in the binary tree.
- Average-case scenario: O(n), where n is the number of nodes in the binary tree.

The reason for this runtime complexity is that DFS explores as far as possible along each branch before backtracking. In a binary tree, each node has at most two children, so the maximum depth of the recursion is logarithmic (O(log n)). However, since we visit each node exactly once, the overall runtime complexity remains O(n).

### Breadth-First Search (BFS):
- Best-case scenario: O(n), where n is the number of nodes in the binary tree.
- Worst-case scenario: O(n), where n is the number of nodes in the binary tree.
- Average-case scenario: O(n), where n is the number of nodes in the binary tree.

The reason for this runtime complexity is that BFS visits all nodes at a given level before moving on to the next level. In a binary tree, each node has at most two children, so the maximum width of the queue (i.e., the number of nodes at a given level) is constant (O(1)). However, since we visit each node exactly once, the overall runtime complexity remains O(n).


## Implementation
### Python
```python
from collections import deque

class Node:
    """A node in the binary tree."""
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None


class BinaryTree:
    """A binary tree implementation."""
    def __init__(self):
        self.root = None

    def insert(self, key):
        """Insert a new key into the tree (level-order insertion for simplicity)."""
        if self.root is None:
            self.root = Node(key)
        else:
            queue = deque([self.root])
            while queue:
                current = queue.popleft()
                if current.left is None:
                    current.left = Node(key)
                    break
                else:
                    queue.append(current.left)
                if current.right is None:
                    current.right = Node(key)
                    break
                else:
                    queue.append(current.right)

    def bfs(self):
        """Perform a Breadth-First Search (level-order traversal)."""
        if not self.root:
            return []

        result = []
        queue = deque([self.root])
        while queue:
            current = queue.popleft()
            result.append(current.key)
            if current.left:
                queue.append(current.left)
            if current.right:
                queue.append(current.right)
        return result

    def dfs_preorder(self):
        """Perform a Depth-First Search (pre-order traversal)."""
        result = []
        self._dfs_preorder(self.root, result)
        return result

    def _dfs_preorder(self, current, result):
        if current:
            result.append(current.key)  # Visit the root
            self._dfs_preorder(current.left, result)  # Traverse left subtree
            self._dfs_preorder(current.right, result)  # Traverse right subtree

    def dfs_inorder(self):
        """Perform a Depth-First Search (in-order traversal)."""
        result = []
        self._dfs_inorder(self.root, result)
        return result

    def _dfs_inorder(self, current, result):
        if current:
            self._dfs_inorder(current.left, result)  # Traverse left subtree
            result.append(current.key)  # Visit the root
            self._dfs_inorder(current.right, result)  # Traverse right subtree

    def dfs_postorder(self):
        """Perform a Depth-First Search (post-order traversal)."""
        result = []
        self._dfs_postorder(self.root, result)
        return result

    def _dfs_postorder(self, current, result):
        if current:
            self._dfs_postorder(current.left, result)  # Traverse left subtree
            self._dfs_postorder(current.right, result)  # Traverse right subtree
            result.append(current.key)  # Visit the root


# Example Usage
bt = BinaryTree()
bt.insert(1)
bt.insert(2)
bt.insert(3)
bt.insert(4)
bt.insert(5)
bt.insert(6)
bt.insert(7)

# Perform BFS and DFS traversals
print("BFS:", bt.bfs())  # Outputs: [1, 2, 3, 4, 5, 6, 7]
print("DFS Pre-Order:", bt.dfs_preorder())  # Outputs: [1, 2, 4, 5, 3, 6, 7]
print("DFS In-Order:", bt.dfs_inorder())  # Outputs: [4, 2, 5, 1, 6, 3, 7]
print("DFS Post-Order:", bt.dfs_postorder())  # Outputs: [4, 5, 2, 6, 7, 3, 1]
```

## Leetcode Questions

### Path (传递) => DFS (recursive)

| # | Problem | Difficulty |
|---|---------|------------|
| 257 | [Binary Tree Paths](../../leetcode_questions/257_binary_tree_paths.md) | Easy |
| 1448 | [Count Good Nodes in Binary Tree](../../leetcode_questions/1448_count_good_nodes_in_binary_tree.md) | Medium |
| 124 | [Binary Tree Maximum Path Sum](../../leetcode_questions/124_binary_tree_maximum_path_sum.md) | Hard |
| 1120 | [Maximum Average Subtree](../../leetcode_questions/1120_maximum_average_subtree.md) | Medium |
| 1372 | [Longest ZigZag Path in a Binary Tree](../../leetcode_questions/1372_longest_zigzag_path_in_a_binary_tree.md) | Medium |
| 1123 | [Lowest Common Ancestor of Deepest Leaves](../../leetcode_questions/1123_lowest_common_ancestor_of_deepest_leaves.md) | Medium |
| 549 | [Binary Tree Longest Consecutive Sequence II](../../leetcode_questions/549_binary_tree_longest_consecutive_sequence_ii.md) | Medium |
