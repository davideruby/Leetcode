## [124. Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

<h2 style="color:#ff375f">Hard</h2>

A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence at most once. Note that the path does not need to pass through the root.

The path sum of a path is the sum of the node's values in the path.

Given the root of a binary tree, return the maximum path sum of any non-empty path.

## Solution
```python
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        self.max_sum = root.val

        def dfs(root):
            if root == None:
                return 0

            left_max = max(0, dfs(root.left))
            right_max = max(0, dfs(root.right))
            self.max_sum = max(self.max_sum, root.val + left_max + right_max) 
            return root.val + max(left_max, right_max)

        dfs(root)
        return self.max_sum
```

## Notes
This problem is such tricky because you have to perform a dfs and keep track of two values instead of just one.

For each visited node, you have to determine the maximum path sum you can get with the node itself, plus the max path sum of both left and right sub-trees (if both left and right values are negative, just discard them and consider only the value of the node).
But, you don't have to return such value to the parent of the node. Rather, you should return the value of the node plus the maximum between the value gotten from the right and the left, because in a path you can't have a split. 
