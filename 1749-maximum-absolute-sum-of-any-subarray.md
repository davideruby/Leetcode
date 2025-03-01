## [1749. Maximum Absolute Sum of Any Subarray](https://leetcode.com/problems/maximum-absolute-sum-of-any-subarray/)

${\textsf{\color{yellow}Medium}}$

Problem description

## Solution
```python
class Solution:
    def maxAbsoluteSum(self, nums: List[int]) -> int:
        max_sum = 0
        cur_sum = 0
        for num in nums:
            if cur_sum < 0:
                cur_sum = 0
            cur_sum += num
            max_sum = max(max_sum, cur_sum)

        cur_sum = 0
        min_sum = 0
        for num in nums:
            if cur_sum > 0:
                cur_sum = 0
            cur_sum += num
            min_sum = min(min_sum, cur_sum)

        return max(max_sum, abs(min_sum))
```

## Notes
Use the Kadane's algorithm to determine the max sum and the min sum. Then return the `max(max_sum, abs(min_sum))`. 
