## [515. Find Largest Value in Each Tree Row](https://leetcode.com/problems/find-largest-value-in-each-tree-row/)

${\textsf{\color{yellow}Medium}}$

Given the root of a binary tree, return an array of the largest value in each row of the tree (0-indexed).

## Solution
```python
from collections import deque

class Solution:
    def largestValues(self, root: Optional[TreeNode]) -> List[int]:
        if root == None:
            return []

        largest_values = []
        queue = deque([root])
        while queue:
            largest = float("-inf")
            for _ in range(len(queue)):
                node = queue.popleft()
                largest = max(largest, node.val)

                for child in [node.left, node.right]:
                    if child:
                        queue.append(child)

            largest_values.append(largest)
        
        return largest_values
```

## Notes
Breadth-First search.
