## [230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

<h2 style="color:#fac31d">Medium</h2>

Given the root of a binary search tree, and an integer k, return the kth smallest value (1-indexed) of all the values of the nodes in the tree.

## Solution
```python
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        stack = []
        idx = 0
        node = root

        while True:
            if node != None:
                stack.append(node)
                node = node.left
            elif len(stack) > 0:
                node = stack.pop()

                idx += 1
                if idx == k:
                    return node.val
                
                node = node.right
            else:
                break
        
        raise Exception(":(")
```

## Notes
An inorder traversal of a binary search tree gives the values in sorted order.
I prefer the iterative version of the inorder traversal to solve this problem.
In fact, you can solve this problem with the recursive versione as well, but you will need some shared variables. 
