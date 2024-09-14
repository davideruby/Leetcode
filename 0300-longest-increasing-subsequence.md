## [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)

<h2 style="color:#fac31d">Medium</h2>

Given an integer array nums, return the length of the longest strictly increasing subsequence.

## Solution
```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        cache = [1] * len(nums)

        for idx in range(len(nums) - 1, -1, -1):
            for jdx in range(idx + 1, len(nums)):
                if nums[jdx] > nums[idx]:
                    cache[idx] = max(cache[idx], 1 + cache[jdx])

        return max(cache)
```

## Notes
This is a dynamic programming problem.

The idea is that longest increasing subsequence starting from element at index `i` is `1 + the longest_increasing_subsequence_at index_j`, for any `j > i` where `nums[i] < nums[j]`.

In order to achieve memoization, you have to store in a `cache` the longest increasing subsequence for each index.
