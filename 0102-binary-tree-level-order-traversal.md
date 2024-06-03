## [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

<h2 style="color:#fac31d">Medium</h2>
Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

## Solution
```python
from collections import deque

class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if root == None:
            return []

        traversal = []
        queue = deque([root])

        while len(queue) > 0:
            level_len = len(queue)
            level = []

            for _ in range(level_len):
                node = queue.popleft()
                level.append(node.val)

                if node.left != None:
                    queue.append(node.left)
                if node.right != None:
                    queue.append(node.right)

            traversal.append(level)
        
        return traversal
```

## Notes
Basically, a breadth-first search of a binary tree.
