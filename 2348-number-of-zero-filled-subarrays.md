## [2348. Number of Zero-Filled Subarrays](https://leetcode.com/problems/number-of-zero-filled-subarrays/)

${\textsf{\color{yellow}Medium}}$

Given an integer array nums, return the number of subarrays filled with 0.

A subarray is a contiguous non-empty sequence of elements within an array.

## Solution
```python
class Solution:
    def zeroFilledSubarray(self, nums: List[int]) -> int:
        current_zeros = 0
        res = 0

        for num in nums:
            if num == 0:
                current_zeros += 1
            else:
                res += (current_zeros * (current_zeros + 1)) // 2
                current_zeros = 0

        res += (current_zeros * (current_zeros + 1)) // 2
        return res
```

## Notes
Sliding window approach.
