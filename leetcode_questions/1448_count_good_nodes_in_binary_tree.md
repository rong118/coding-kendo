# 1448. Count Good Nodes in Binary Tree

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/count-good-nodes-in-binary-tree/)

## Question Description
Given a binary tree root, a node X in the tree is named good if in the path from root to X there are no nodes with a value greater than X.

Return the number of good nodes in the binary tree.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/04/02/test_sample_1.png" width="400" />
>
> Input: root = [3,1,4,3,null,1,5]
>
> Output: 4
>
> Explanation: Nodes in blue are good.
>
> Root Node (3) is always a good node.
>
> Node 4 -> (3,4) is the maximum value in the path starting from the root.
>
> Node 5 -> (3,4,5) is the maximum value in the path
>
> Node 3 -> (3,1,3) is the maximum value in the path.

Example 2:
> <img src="https://assets.leetcode.com/uploads/2020/04/02/test_sample_2.png" width="400" />
>
> Input: root = [3,3,null,4,2]
>
> Output: 3
>
> Explanation: Node 2 -> (3, 3, 2) is not good, because "3" is higher than it.

Example 3:
>
> Input: root = [1]
>
> Output: 1
>
> Explanation: Root is considered as good.

<br/>

Constraints:
- The number of nodes in the binary tree is in the range [1, 10^5].
- Each node's value is between [-10^4, 10^4].

## Tags
- tree
- dfs

## Approach
**Key idea:** A node is good exactly when its value is at least the maximum value seen on the path from the root, so a DFS only needs to carry that running maximum down.

1. Start a DFS at the root with `path_max = -inf` (an explicit stack of `(node, path_max)` pairs avoids deep recursion).
2. If `node.val >= path_max`, count the node and update `path_max = node.val`.
3. Push both children with the (possibly updated) `path_max`.
4. Return the total count once the stack is empty.

## Code Implementation
```python
from typing import Optional

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def goodNodes(self, root: TreeNode) -> int:
        # iterative DFS: Python's recursion limit is too small for a 10^5-node skewed tree
        count = 0
        stack: list[tuple[Optional[TreeNode], float]] = [(root, float("-inf"))]
        while stack:
            node, path_max = stack.pop()
            if not node:
                continue
            if node.val >= path_max:
                count += 1
                path_max = node.val
            stack.append((node.left, path_max))
            stack.append((node.right, path_max))
        return count
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node is visited once
>
> Space complexity : O(h) — explicit DFS stack; O(n) worst case for a skewed tree

## Related Problems
- [124. Binary Tree Maximum Path Sum](./124_binary_tree_maximum_path_sum.md) — 🔴 Hard · DFS carrying path information
- [257. Binary Tree Paths](./257_binary_tree_paths.md) — 🟢 Easy · root-to-leaf path DFS
- [98. Validate Binary Search Tree](./98_validate_binary_search_tree.md) — 🟡 Medium · passing bounds down a DFS
- [1372. Longest ZigZag Path in a Binary Tree](./1372_longest_zigzag_path_in_a_binary_tree.md) — 🟡 Medium · DFS with state passed from parent
