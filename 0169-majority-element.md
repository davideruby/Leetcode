## [169. Majority Element](https://leetcode.com/problems/majority-element/)

${\textsf{\color{green}Easy}}$

Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

## Solution
```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        nums.sort()
        return nums[len(nums) // 2]
```
