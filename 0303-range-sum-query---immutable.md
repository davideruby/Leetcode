## [303. Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/)

<h2 style="color:#00b8a3">Easy</h2>

Given an integer array nums, handle multiple queries of the following type:

1. Calculate the sum of the elements of nums between indices left and right inclusive where left <= right.


Implement the NumArray class:

- NumArray(int[] nums) Initializes the object with the integer array nums.
- int sumRange(int left, int right) Returns the sum of the elements of nums between indices left and right inclusive (i.e. nums[left] + nums[left + 1] + ... + nums[right]).

## Solution
```python
class NumArray:

    def __init__(self, nums: List[int]):
        self.prefix_sums = {-1: 0}
        current_sum = 0
        for idx, num in enumerate(nums):
            current_sum += num
            self.prefix_sums[idx] = current_sum

    def sumRange(self, left: int, right: int) -> int:
        return self.prefix_sums[right] - self.prefix_sums[left - 1]
```

## Notes
Store prefix sums.
