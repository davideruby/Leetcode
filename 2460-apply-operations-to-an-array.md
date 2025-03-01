## [2460. Apply Operations to an Array](https://leetcode.com/problems/apply-operations-to-an-array/)

${\textsf{\color{green}Easy}}$

You are given a 0-indexed array nums of size n consisting of non-negative integers.

You need to apply n - 1 operations to this array where, in the ith operation (0-indexed), you will apply the following on the ith element of nums:

- If nums[i] == nums[i + 1], then multiply nums[i] by 2 and set nums[i + 1] to 0. Otherwise, you skip this operation.

After performing all the operations, shift all the 0's to the end of the array.

- For example, the array [1,0,2,0,0,1] after shifting all its 0's to the end, is [1,2,1,0,0,0].

Return the resulting array.

Note that the operations are applied sequentially, not all at once.

## Solution
```python
class Solution:
    def applyOperations(self, nums: List[int]) -> List[int]:
        for idx in range(len(nums) - 1):
            if nums[idx] == nums[idx + 1]:
                nums[idx] *= 2
                nums[idx + 1] = 0
        
        idx_zero = 0
        for idx in range(len(nums)):
            if nums[idx] != 0:
                nums[idx_zero], nums[idx] = nums[idx], nums[idx_zero]
                idx_zero += 1
        
        return nums
```
