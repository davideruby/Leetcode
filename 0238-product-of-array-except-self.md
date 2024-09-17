## [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)

<h2 style="color:#fac31d">Medium</h2>

Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.

## Solution
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        prefix = 1
        answer = [0] * len(nums)
        for idx in range(len(nums)):
            answer[idx] = prefix
            prefix *= nums[idx]

        suffix = 1
        for idx in range(len(nums) - 1, -1, -1):
            answer[idx] *= suffix
            suffix *= nums[idx]

        return answer
```

## Notes
Use two variables, `prefix` and `suffix`, to store the products from left-to-right and from right-to-left.
