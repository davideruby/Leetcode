## [3356. Zero Array Transformation II](https://leetcode.com/problems/zero-array-transformation-ii/)

${\textsf{\color{yellow}Medium}}$

You are given an integer array nums of length n and a 2D array queries where queries[i] = [li, ri, vali].

Each queries[i] represents the following action on nums:

- Decrement the value at each index in the range [li, ri] in nums by at most vali.
- The amount by which each value is decremented can be chosen independently for each index.

A Zero Array is an array with all its elements equal to 0.

Return the minimum possible non-negative value of k, such that after processing the first k queries in sequence, nums becomes a Zero Array. If no such k exists, return -1.

## Solution
```python
class Solution:
    def minZeroArray(self, nums: List[int], queries: List[List[int]]) -> int:
        left = 0
        right = len(queries)
        res = -1

        while left <= right:
            num_moves = (left + right) // 2

            if self.canMakeZeroArrayInNumMoves(nums, queries, num_moves):
                res = num_moves
                right = num_moves - 1
            else:
                left = num_moves + 1
        
        return res


    def canMakeZeroArrayInNumMoves(self, nums, queries, numMoves):
        diff = [0] * (len(nums) + 1)

        for idx in range(numMoves):
            left, right, val = queries[idx]
            diff[left] += val
            diff[right + 1] -= val

        for idx in range(len(nums)):
            if idx > 0:
                diff[idx] += diff[idx - 1]
            if diff[idx] < nums[idx]:
                return False

        return True
```

## Notes
The `canMakeZeroArrayInNumMoves()` function uses the same approach described in [3355. Zero Array Transformation I](./3355-zero-array-transformation-i.md).
Then, to speed up the solution, use a binary search to get the minimum number of moves necessary to make a zero array.
