## [1448. Count Good Nodes in Binary Tree](https://leetcode.com/problems/count-good-nodes-in-binary-tree/)

<h2 style="color:#fac31d">Medium</h2>
Given a binary tree root, a node X in the tree is named good if in the path from root to X there are no nodes with a value greater than X.

Return the number of good nodes in the binary tree.

## Solution
```python
class Solution:
    def goodNodes(self, root: TreeNode) -> int:

        def dfs(root: TreeNode, max_parent_value: int) -> int:
            if root == None:
                return 0
        
            max_value = max(max_parent_value, root.val)
            left_good_nodes = dfs(root.left, max_value)
            right_good_nodes = dfs(root.right, max_value)

            good_nodes = left_good_nodes + right_good_nodes
            is_good_node = root.val >= max_value
            if is_good_node:
                good_nodes += 1

            return good_nodes
        
        return dfs(root, root.val)
```

## Notes
Probably, it could be labeled as Easy. 
Just perform a dfs (a preorder visit to be precise) taking into account the `max_parent_value`.
