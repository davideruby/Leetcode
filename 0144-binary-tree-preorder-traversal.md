## [144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)

${\textsf{\color{green}Easy}}$

Given the root of a binary tree, return the preorder traversal of its nodes' values.

## Solution
```python
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        traversal = []
        self.preorderTraversalRec(root, traversal)
        return traversal

    def preorderTraversalRec(self, root, traversal):
        if root == None:
            return

        traversal.append(root.val)
        self.preorderTraversalRec(root.left, traversal)
        self.preorderTraversalRec(root.right, traversal)
```
