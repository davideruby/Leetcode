## [136. Single Number](https://leetcode.com/problems/single-number/)

${\textsf{\color{green}Easy}}$

Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

## Solution
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        res = 0

        for num in nums:
            res = res ^ num

        return res
```
