# 173. Binary Search Tree Iterator

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/binary-search-tree-iterator/)

## Question Description
Implement the BSTIterator class that represents an iterator over the in-order traversal of a binary search tree (BST):

- BSTIterator(TreeNode root) Initializes an object of the BSTIterator class. The root of the BST is given as part of the constructor. The pointer should be initialized to a non-existent number smaller than any element in the BST.
- boolean hasNext() Returns true if there exists a number in the traversal to the right of the pointer, otherwise returns false.
int next() Moves the pointer to the right, then returns the number at the pointer.
- Notice that by initializing the pointer to a non-existent smallest number, the first call to next() will return the smallest element in the BST.

You may assume that next() calls will always be valid. That is, there will be at least a next number in the in-order traversal when next() is called.
<br/>
<br/>
Example 1:
> <img src="https://assets.leetcode.com/uploads/2018/12/25/bst-tree.png" width="400" />
>
> Input
>
> ["BSTIterator", "next", "next", "hasNext", "next", "hasNext", "next", "hasNext", "next", "hasNext"]
>
> [[[7, 3, 15, null, null, 9, 20]], [], [], [], [], [], [], [], [], []]
>
> Output
>
> [null, 3, 7, true, 9, true, 15, true, 20, false]

> Explanation
>
> BSTIterator bSTIterator = new BSTIterator([7, 3, 15, null, null, 9, 20]);
>
> bSTIterator.next();    // return 3
>
> bSTIterator.next();    // return 7
>
> bSTIterator.hasNext(); // return True
>
> bSTIterator.next();    // return 9
>
> bSTIterator.hasNext(); // return True
>
> bSTIterator.next();    // return 15
>
> bSTIterator.hasNext(); // return True
>
> bSTIterator.next();    // return 20
>
> bSTIterator.hasNext(); // return False

Constraints:
- The number of nodes in the tree is in the range [1, 10<sup>5</sup> ].
- 0 <= Node.val <= 10<sup>6</sup> 
- At most 10<sup>5</sup>  calls will be made to hasNext, and next.

Follow up:
Could you implement next() and hasNext() to run in average O(1) time and use O(h) memory, where h is the height of the tree?

## Tags
- tree

## Approach
**Key idea:** Run the iterative inorder traversal lazily — a stack holds the path of pending ancestors, so the top is always the next smallest value.

1. On construction, push `root` and all of its left descendants onto the stack.
2. `next()`: pop the top node; it is the smallest unvisited value.
3. Before returning, push the popped node's right child and all of that child's left descendants.
4. `hasNext()`: return whether the stack is non-empty.
5. Each node is pushed and popped exactly once, so `next()` is O(1) amortized.

## Code Implementation
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class BSTIterator:
    def __init__(self, root: Optional[TreeNode]):
        self.stack: list[TreeNode] = []
        self._push_all_left(root)

    def next(self) -> int:
        node = self.stack.pop()
        self._push_all_left(node.right)
        return node.val

    def hasNext(self) -> bool:
        return bool(self.stack)

    def _push_all_left(self, node: Optional[TreeNode]) -> None:
        while node:
            self.stack.append(node)
            node = node.left
```

## Time Complexity Analysis
> Time complexity  : O(1) amortized for next(), O(1) for hasNext()
>
> Space complexity : O(h) — the stack holds at most one root-to-leaf path

## Related Problems
- [94. Binary Tree Inorder Traversal](./94_binary_tree_inorder_traversal.md) — 🟢 Easy · the same iterative inorder traversal
- [98. Validate Binary Search Tree](./98_validate_binary_search_tree.md) — 🟡 Medium · inorder of a BST is sorted
- [426. Convert Binary Search Tree to Sorted Doubly Linked List](./426_convert_binary_search_tree_to_sorted_doubly_linked_list.md) — 🟡 Medium · walk a BST in sorted order
