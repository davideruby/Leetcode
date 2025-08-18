## [404. Sum of Left Leaves](https://leetcode.com/problems/sum-of-left-leaves/)

${\textsf{\color{green}Easy}}$

Given the root of a binary tree, return the sum of all left leaves.

A leaf is a node with no children. A left leaf is a leaf that is the left child of another node.

## Solution
```python
class Solution:
    def sumOfLeftLeaves(self, root: Optional[TreeNode]) -> int:
        return self.helper(root, "right")

    def helper(self, root, parent):
        if root == None:
            return 0

        if root.left == root.right == None and parent == "left":
            return root.val

        return self.helper(root.left, "left") + self.helper(root.right, "right")
```

## Notes
It took me a while to be honest, even though it is an easy. Perform a DFS with a flag telling whether the parent called the recursive method to its left or right child.
