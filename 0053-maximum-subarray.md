## [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

<h2 style="color:#fac31d">Medium</h2>

Given an integer array nums, find the subarray with the largest sum, and return its sum.

## Solution
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        current_sum = 0
        largest_sum = nums[0]

        for num in nums:
            if current_sum < 0:
                current_sum = 0
            current_sum += num

            if current_sum > largest_sum:
                largest_sum = current_sum

        return largest_sum
```

## Notes
Kadane's algorithm. We use a for loop to get the current sum. The key is that when the current sum is less than 0, it makes no sense to consider the sum of the previous elements, so we throw them away and we restart our sum from zero.
