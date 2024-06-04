## [110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/description/)

<h2 style="color:#00b8a3">Easy</h2>

Given a binary tree, determine if it is height-balanced.

## Solution
```python
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:

        def dfs(root: Optional[TreeNode]) -> Tuple[int, bool]:
            if root == None:
                return 0, True

            left_height, left_is_balanced = dfs(root.left)
            right_height, right_is_balanced = dfs(root.right)

            height = 1 + max(left_height, right_height)
            is_balanced = abs(left_height - right_height) <= 1 and left_is_balanced and right_is_balanced

            return height, is_balanced

        height, is_balanced = dfs(root)
        return is_balanced
```

## Notes
Perform depth-first search to determine the height of each sub-tree and if it is balanced.
