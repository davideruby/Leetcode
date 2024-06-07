## [572. Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/)

<h2 style="color:#00b8a3">Easy</h2>

Given the roots of two binary trees root and subRoot, return true if there is a subtree of root with the same structure and node values of subRoot and false otherwise.

A subtree of a binary tree tree is a tree that consists of a node in tree and all of this node's descendants. The tree tree could also be considered as a subtree of itself.

## Solution
```python
class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        
        def sameTree(root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
            if root == None or subRoot == None:
                return root == subRoot == None
            
            return root.val == subRoot.val and sameTree(root.left, subRoot.left) and sameTree(root.right, subRoot.right)

        if root == None:
            return False
        
        if sameTree(root, subRoot):
            return True
        
        return self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)
```

## Notes
First of all, you have to understand the difference between sameTree and subTree. SameTree means that the two trees are exactly the equal in their values. SubTree means that a subtree of `root` is the same as `subRoot`.
So, define sameTree() function, and then discover if such a subtree of `root` exists.
