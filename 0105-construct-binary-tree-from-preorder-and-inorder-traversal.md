## [105. Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

<h2 style="color:#fac31d">Medium</h2>

Given two integer arrays preorder and inorder where preorder is the preorder traversal of a binary tree and inorder is the inorder traversal of the same tree, construct and return the binary tree.

## Solution
```python
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        if len(preorder) == 0 or len(inorder) == 0:
            return None

        val = preorder[0]
        root = TreeNode(val)
        inorder_val_idx = inorder.index(val)
        root.left = self.buildTree(preorder[1:inorder_val_idx + 1], inorder[:inorder_val_idx + 1])
        root.right = self.buildTree(preorder[inorder_val_idx + 1:], inorder[inorder_val_idx + 1:])
        return root
```

## Notes
I found this problem hard. You have to deeply think by recursion to understand the solution of this problem.

`preorder[0]` is the key of the current root node. We find the index of `preorder[0]` in `inorder`, say it's `in[4]`.
This means that everything between `in[0]` and `in[4]` stands on the left side, and everything from `in[5]` to the end stands to the right side
