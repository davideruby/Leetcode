## [268. Missing Number](https://leetcode.com/problems/missing-number/)

${\textsf{\color{green}Easy}}$

Given an array nums containing n distinct numbers in the range [0, n], return the only number in the range that is missing from the array.

## Solution
```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        missing = 0

        for num in list(range(len(nums) + 1)):
            missing = missing ^ num
        
        for num in nums:
            missing = missing ^ num

        return missing
```

## Notes
We take the XOR of the given array and the first `n` number.
