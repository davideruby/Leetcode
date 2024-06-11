## [78. Subsets](https://leetcode.com/problems/subsets/)

<h2 style="color:#fac31d">Medium</h2>

Given an integer array nums of unique elements, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

## Solution
```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        subsets = []
        self.subsetsHelper(nums, subsets, [False] * len(nums), 0)
        return subsets
        
    def subsetsHelper(self, nums: List[int], subsets: List[int], takes: List[bool], idx: int) -> None:
        if idx == len(nums):
            subset = []
            for jdx in range(len(nums)):
                if takes[jdx]:
                    subset.append(nums[jdx])
            subsets.append(subset)
        else:
            takes[idx] = False  # take nums[idx]
            self.subsetsHelper(nums, subsets, takes, idx + 1)
            takes[idx] = True  # don't take nums[idx]
            self.subsetsHelper(nums, subsets, takes, idx + 1)
```
