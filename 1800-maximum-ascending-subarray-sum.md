## [1800. Maximum Ascending Subarray Sum](https://leetcode.com/problems/maximum-ascending-subarray-sum/)

${\textsf{\color{green}Easy}}$

Given an array of positive integers nums, return the maximum possible sum of an ascending subarray in nums.

A subarray is defined as a contiguous sequence of numbers in an array.

A subarray [numsl, numsl+1, ..., numsr-1, numsr] is ascending if for all i where l <= i < r, numsi  < numsi+1. Note that a subarray of size 1 is ascending.

## Solution
```python
class Solution:
    def maxAscendingSum(self, nums: List[int]) -> int:
        max_sum = nums[0]
        current_sum = nums[0]

        for idx in range(1, len(nums)):
            if nums[idx - 1] >= nums[idx]:
                current_sum = 0
                
            current_sum += nums[idx]
            max_sum = max(max_sum, current_sum)

        return max_sum
```

## Notes
Kinda similar to the Kadane's algo.
