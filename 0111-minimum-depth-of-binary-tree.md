## [111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)

<h2 style="color:#00b8a3">Easy</h2>

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Note: A leaf is a node with no children.

## Solution
```python
class Solution:
    def minDepth(self, root: Optional[TreeNode]) -> int:
        if root == None:
            return 0
        
        if root.left == root.right == None:
            return 1

        left = self.minDepth(root.left) if root.left else float("inf")
        right = self.minDepth(root.right) if root.right else float("inf")
        return 1 + min(left, right)
```
