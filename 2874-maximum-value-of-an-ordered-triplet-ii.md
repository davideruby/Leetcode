## [2874. Maximum Value of an Ordered Triplet II](https://leetcode.com/problems/maximum-value-of-an-ordered-triplet-ii/)

${\textsf{\color{yellow}Medium}}$

You are given a 0-indexed integer array nums.

Return the maximum value over all triplets of indices (i, j, k) such that i < j < k. If all such triplets have a negative value, return 0.

The value of a triplet of indices (i, j, k) is equal to (nums[i] - nums[j]) * nums[k].

## Solution
```python
class Solution:
    def maximumTripletValue(self, nums: List[int]) -> int:
        max_triplet = 0
        max_diff = 0
        max_num = 0

        for num in nums:
            max_triplet = max(max_triplet, max_diff * num)
            max_num = max(max_num, num)
            max_diff = max(max_diff, max_num - num)

        return max_triplet
```

## Notes
This is a greedy solution. 

We have to find the maximum triplet `(nums[i] - nums[j]) * nums[k]`.
So, we have to find the maximum difference we can find in our array. To do so, we keep track of two values: `max_num` (i.e. the maximum `num` found so far) and `max_diff` (i.e. the maximum difference found so far, it can be expressed as `max_num - nums[i]`).
Then, we also have to store the maximum triplet value, as: `max_diff * nums[i]`.