## [226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)

<h2 style="color:#00b8a3">Easy</h2>

Given the root of a binary tree, invert the tree, and return its root.

## Solution
```python
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]: 
        if root == None:
            return None
        
        root.left, root.right = root.right, root.left
        self.invertTree(root.left)
        self.invertTree(root.right)
        return root
```

