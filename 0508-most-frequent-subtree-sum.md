## [508. Most Frequent Subtree Sum](https://leetcode.com/problems/most-frequent-subtree-sum/)

${\textsf{\color{yellow}Medium}}$

Given the root of a binary tree, return the most frequent subtree sum. If there is a tie, return all the values with the highest frequency in any order.

The subtree sum of a node is defined as the sum of all the node values formed by the subtree rooted at that node (including the node itself).

## Solution
```python
class Solution:
    def findFrequentTreeSum(self, root: Optional[TreeNode]) -> List[int]:
        sum_counts = {}
        self.subTreeSum(root, sum_counts)
        
        max_count = max(sum_counts.values())
        return [value for value, count in sum_counts.items() if count == max_count]

    def subTreeSum(self, root, sum_counts):
        if root == None:
            return 0

        sub_tree_sum = root.val + self.subTreeSum(root.left, sum_counts) + self.subTreeSum(root.right, sum_counts)

        sum_counts[sub_tree_sum] = sum_counts.get(sub_tree_sum, 0) + 1
        return sub_tree_sum
```

## Notes
Depth-First search + hashmap.
