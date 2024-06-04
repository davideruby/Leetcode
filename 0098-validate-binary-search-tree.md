## [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)

<h2 style="color:#fac31d">Medium</h2>
Given the root of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:

- The left subtree of a node contains only nodes with keys less than the node's key.
- The right subtree of a node contains only nodes with keys greater than the node's key.
- Both the left and right subtrees must also be binary search trees.

## Solution
```python
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        
        def dfs(root: Optional[TreeNode], min_val: int, max_val: int) -> bool:
            if root == None:
                return True

            is_valid = min_val < root.val < max_val
            return is_valid and dfs(root.left, min_val, root.val) and dfs(root.right, root.val, max_val)

        return dfs(root, float("-infinity"), float("infinity"))
```

## Notes
There two main solutions for this problem:
- The first solution is the one here, which checks if each node value is in the correct range.
- The second one is more trivial: just perform an inorder traversal and check the values are in sorted order.