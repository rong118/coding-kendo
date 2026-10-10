# Tree Traversal

There are several ways to traverse a tree data structure, depending on the order in which you want to visit the nodes

## I. Pre-order traversal
Visit the current node first, then recursively traverse the left subtree, and finally traverse the right subtree.

Example: In a binary tree, visit the root node, then the left child, then the right child.

### Implementation
```python
def preorder_traversal(self):
    """Perform a preorder traversal of the BST."""
    result = []
    self._preorder_traversal(self.root, result)
    return result

def _preorder_traversal(self, current, result):
    if current is not None:
        result.append(current.key)  # Visit the root
        self._preorder_traversal(current.left, result)  # Traverse left subtree
        self._preorder_traversal(current.right, result)  # Traverse right subtree
```

## II. In-order traversal
Traverse the left subtree, then visit the current node, and finally traverse the right subtree.

Example: In a binary tree, visit the left child of the root, then the root itself, then the right child.

### Implementation
```python
def inorder_traversal(self):
    """Perform an in-order traversal of the BST."""
    result = []
    self._inorder_traversal(self.root, result)
    return result

def _inorder_traversal(self, current, result):
    if current is not None:
        self._inorder_traversal(current.left, result)  # Traverse left subtree
        result.append(current.key)  # Visit the root
        self._inorder_traversal(current.right, result)  # Traverse right subtree
```

## III. Post-order traversal
Traverse the left subtree, then traverse the right subtree, and finally visit the current node.

Example: In a binary tree, visit the left child of the root, then the right child, then the root itself.

### Implementation
```python
def postorder_traversal(self):
    """Perform a post-order traversal of the BST."""
    result = []
    self._postorder_traversal(self.root, result)
    return result

def _postorder_traversal(self, current, result):
    if current is not None:
        self._postorder_traversal(current.left, result)  # Traverse left subtree
        self._postorder_traversal(current.right, result)  # Traverse right subtree
        result.append(current.key)  # Visit the root
```

## IV. Runtime Complexity
The runtime complexity of traversing a binary tree (pre-order, in-order, or post-order) is **O(n)**, where n is the number of nodes in the tree. 

This is because, in each traversal method, every node in the tree is visited exactly once

## Leetcode Questions

### 遍历

| # | Problem | Difficulty |
|---|---------|------------|
| 144 | [Binary Tree Preorder Traversal](../../leetcode_questions/144_binary_tree_preorder_traversal.md) | Easy |
| 94 | [Binary Tree Inorder Traversal](../../leetcode_questions/94_binary_tree_inorder_traversal.md) | Easy |
| 145 | [Binary Tree Postorder Traversal](../../leetcode_questions/145_binary_tree_postorder_traversal.md) | Easy |
| 102 | [Binary Tree Level Order Traversal](../../leetcode_questions/102_binary_tree_level_order_traversal.md) | Medium |
| 103 | [Binary Tree Zigzag Level Order Traversal](../../leetcode_questions/103_binary_tree_zigzig_level_order_traversal.md) | Medium |
| 107 | [Binary Tree Level Order Traversal II](../../leetcode_questions/107_binary_tree_level_order_traversal_II.md) | Medium |
| 314 | [Binary Tree Vertical Order Traversal](../../leetcode_questions/314_binary_tree_vertical_order_traversal.md) | Medium |
| 987 | [Vertical Order Traversal of a Binary Tree](../../leetcode_questions/987_vertical_order_traversal_of_a_binary_tree.md) | Hard |

### 结构转换/序列化

| # | Problem | Difficulty |
|---|---------|------------|
| 297 | [Serialize and Deserialize Binary Tree](../../leetcode_questions/297_serialize_and_deserialize_binary_tree.md) | Hard |
| 428 | [Serialize and Deserialize N-ary Tree](../../leetcode_questions/428_serialize_and_deserialize_nary_tree.md) | Hard |
| 449 | [Serialize and Deserialize BST](../../leetcode_questions/449_serialize_and_deserialize_BST.md) | Medium |
| 1008 | [Construct Binary Search Tree from Preorder Traversal](../../leetcode_questions/1008_construct_binary_search_tree_from_preorder_traversal.md) | Medium |
| 105 | [Construct Binary Tree from Preorder and Inorder Traversal](../../leetcode_questions/105_construct_binary_tree_from_preorder_and_inorder_traversal.md) | Medium |
| 106 | [Construct Binary Tree from Inorder and Postorder Traversal](../../leetcode_questions/106_construct_binary_tree_from_inorder_and_postorder_traversal.md) | Medium |
| 889 | [Construct Binary Tree from Preorder and Postorder Traversal](../../leetcode_questions/889_construct_binary_tree_from_preorder_and_postorder_traversal.md) | Medium |
| 426 | [Convert Binary Search Tree to Sorted Doubly Linked List](../../leetcode_questions/426_convert_binary_search_tree_to_sorted_doubly_linked_list.md) | Medium |
