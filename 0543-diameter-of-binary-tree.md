## [543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

<h2 style="color:#00b8a3">Easy</h2>
Given the root of a binary tree, return the length of the diameter of the tree.

The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

The length of a path between two nodes is represented by the number of edges between them.

## Solution
```python
class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        height, diameter = self.helperDfs(root)
        return diameter

    def helperDfs(self, root: Optional[TreeNode]) -> Tuple[int, int]:
        if root == None:
            return 0, 0
        
        left_height, left_diameter = self.helperDfs(root.left)
        right_height, right_diameter = self.helperDfs(root.right)

        height = 1 + max(left_height, right_height)
        diameter = max(left_diameter, right_diameter, left_height + right_height)
        return height, diameter
```

## Notes
Not so easy in my honest opinion. 
The important point in my algorithm is that the diameter of a node is: `max(left_diameter, right_diameter, left_height + right_height)`. So, I used a helper function to calculate height and diameter at the same time.
