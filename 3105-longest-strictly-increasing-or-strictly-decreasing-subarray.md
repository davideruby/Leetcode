## [3105. Longest Strictly Increasing or Strictly Decreasing Subarray](https://leetcode.com/problems/longest-strictly-increasing-or-strictly-decreasing-subarray/)

${\textsf{\color{green}Easy}}$

You are given an array of integers nums. Return the length of the longest 
subarray of nums which is either strictly increasing or strictly decreasing.

## Solution
```python
class Solution:
    def longestMonotonicSubarray(self, nums: List[int]) -> int:
        increasing = 1
        decreasing = 1
        max_monotonic = 1

        for idx in range(1, len(nums)):
            if nums[idx] > nums[idx - 1]:
                increasing += 1
            else:
                increasing = 1

            if nums[idx] < nums[idx - 1]:
                decreasing += 1
            else:
                decreasing = 1

            max_monotonic = max(max_monotonic, increasing, decreasing)
        
        return max_monotonic
```
