## [46. Permutations](https://leetcode.com/problems/permutations/)

<h2 style="color:#fac31d">Medium</h2>

Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

## Solution
```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        permutations = []
        self.permuteHelper(nums, permutations, 0)
        return permutations


    def permuteHelper(self, nums: List[int], permutations: List[List[int]], idx: int) -> None:
        if idx == len(nums):
            permutations.append(nums.copy())
            return
        
        for jdx in range(idx, len(nums)):
            nums[jdx], nums[idx] = nums[idx], nums[jdx]
            self.permuteHelper(nums, permutations, idx + 1)
            nums[jdx], nums[idx] = nums[idx], nums[jdx]
```

## Notes
Let's take as example the set {a, b, c, d}.
So, the permutations of {a, b, c, d} is:
- a plus the permutations of {b, c, d},
- b plus the permutations of {a, c, d},
- c plus the permutations of {a, b, d},
- d plus the permutations of {a, b, c}. 
