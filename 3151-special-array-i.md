## [3151. Special Array I](https://leetcode.com/problems/special-array-i/)

${\textsf{\color{green}Easy}}$

An array is considered special if every pair of its adjacent elements contains two numbers with different parity.

You are given an array of integers nums. Return true if nums is a special array, otherwise, return false.

## Solution
```python
class Solution:
    def isArraySpecial(self, nums: List[int]) -> bool:
        for idx in range(1, len(nums)):
            if nums[idx - 1] % 2 == nums[idx] % 2:
                return False

        return True
```
