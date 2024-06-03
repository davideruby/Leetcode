## [199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/description/)

<h2 style="color:#fac31d">Medium</h2>
Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

## Solution
```python
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        if root == None:
            return []

        right_side_view = []
        queue = collections.deque([root])

        while len(queue) > 0:
            queue_len = len(queue)
            for idx in range(queue_len):
                node = queue.popleft()

                if node.left != None:
                    queue.append(node.left)
                if node.right != None:
                    queue.append(node.right)

                if idx == queue_len - 1:
                    right_side_view.append(node.val)
        
        return right_side_view
```

## Notes
Slightly modify a breadth-first search of a binary tree.
