## [2873. Maximum Value of an Ordered Triplet I](https://leetcode.com/problems/maximum-value-of-an-ordered-triplet-i/)

${\textsf{\color{green}Easy}}$

You are given a 0-indexed integer array nums.

Return the maximum value over all triplets of indices (i, j, k) such that i < j < k. If all such triplets have a negative value, return 0.

The value of a triplet of indices (i, j, k) is equal to (nums[i] - nums[j]) * nums[k].

## Solution
```python
class Solution:
    def maximumTripletValue(self, nums: List[int]) -> int:
        max_value = 0

        for idx in range(len(nums)):
            for jdx in range(idx + 1, len(nums)):
                for kdx in range(jdx + 1, len(nums)):
                    max_value = max(max_value, (nums[idx] - nums[jdx]) * nums[kdx])

        return max_value
```

## Notes
This is the easy solution where the brute force O(n^3) solution is allowed. If you want the optimal solution which has O(n) time complexity, see [2874. Maximum Value of an Ordered Triplet II](./2874-maximum-value-of-an-ordered-triplet-ii.md)
