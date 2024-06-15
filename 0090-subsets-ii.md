## [90. Subsets II](https://leetcode.com/problems/subsets-ii/)

<h2 style="color:#fac31d">Medium</h2>

Given an integer array nums that may contain duplicates, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

## Solution
```python
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        subsets = []
        self.subsetsWithDupHelper(nums, subsets, [], 0)
        return subsets    
    

    def subsetsWithDupHelper(self, nums:List[int], subsets: List[List[int]], current: List[int], idx: int) -> None:
        if idx == len(nums):
            subsets.append(current.copy())
            return
        
        # include nums[idx]
        current.append(nums[idx])
        self.subsetsWithDupHelper(nums, subsets, current, idx + 1)

        # do not include any number equal to nums[idx]
        current.pop()
        while idx < len(nums) - 1 and nums[idx] == nums[idx + 1]:
            idx += 1
        self.subsetsWithDupHelper(nums, subsets, current, idx + 1)
```

## Notes
In addition to [78. Subsets](https://leetcode.com/problems/subsets/), you sort the `nums` array and when you have not to include `nums[idx]` in the solution, you have to increase `idx` until you find a different number.