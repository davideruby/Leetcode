## [3191. Minimum Operations to Make Binary Array Elements Equal to One I](https://leetcode.com/problems/minimum-operations-to-make-binary-array-elements-equal-to-one-i/)

${\textsf{\color{yellow}Medium}}$

You are given a binary array nums.

You can do the following operation on the array any number of times (possibly zero):

- Choose any 3 consecutive elements from the array and flip all of them.

Flipping an element means changing its value from 0 to 1, and from 1 to 0.

Return the minimum number of operations required to make all elements in nums equal to 1. If it is impossible, return -1.

## Solution
```python
class Solution:
    def minOperations(self, nums: List[int]) -> int:
        num_ops = 0

        for idx in range(len(nums) - 2):
            if nums[idx] == 0:
                for jdx in range(3):
                    nums[idx + jdx] = 1 if nums[idx + jdx] == 0 else 0
            
                num_ops += 1
        
        return num_ops if nums[-1] == nums[-2] == 1 else -1
```

## Notes
The easiest solution is sometimes the best solution.
