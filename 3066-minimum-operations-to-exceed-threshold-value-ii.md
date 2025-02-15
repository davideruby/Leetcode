## [3066. Minimum Operations to Exceed Threshold Value II](https://leetcode.com/problems/minimum-operations-to-exceed-threshold-value-ii/)

${\textsf{\color{yellow}Medium}}$

You are given a 0-indexed integer array nums, and an integer k.

You are allowed to perform some operations on nums, where in a single operation, you can:

- Select the two smallest integers x and y from nums.
- Remove x and y from nums.
- Insert (min(x, y) * 2 + max(x, y)) at any position in the array.

Note that you can only apply the described operation if nums contains at least two elements.

Return the minimum number of operations needed so that all elements of the array are greater than or equal to k.

## Solution
```python
import heapq

class Solution:
    def minOperations(self, nums: List[int], k: int) -> int:
        heapq.heapify(nums)
        num_ops = 0

        while nums[0] < k:
            heapq.heappush(nums, heapq.heappop(nums) * 2 + heapq.heappop(nums))
            num_ops += 1

        return num_ops
```

## Notes
Use a min-heap to get the first two smallest elements in O(log n) time.
