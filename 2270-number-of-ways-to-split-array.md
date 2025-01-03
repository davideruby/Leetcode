## [2270. Number of Ways to Split Array](https://leetcode.com/problems/number-of-ways-to-split-array/)

${\textsf{\color{yellow}Medium}}$

You are given a 0-indexed integer array nums of length n.

nums contains a valid split at index i if the following are true:

- The sum of the first i + 1 elements is greater than or equal to the sum of the last n - i - 1 elements.
- There is at least one element to the right of i. That is, 0 <= i < n - 1.

Return the number of valid splits in nums.

## Solution
```python
class Solution:
    def waysToSplitArray(self, nums: List[int]) -> int:
        right = sum(nums)
        left = 0
        splits = 0

        for idx in range(len(nums) - 1):
            left += nums[idx]
            right -= nums[idx]
            
            if left >= right:
                splits += 1

        return splits
```

## Notes
Precompute the total sum of the array.
