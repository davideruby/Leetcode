## [55. Jump Game](https://leetcode.com/problems/jump-game/)

<h2 style="color:#fac31d">Medium</h2>

You are given an integer array nums. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position.

Return true if you can reach the last index, or false otherwise.

## Solution
```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        max_reach = 0

        for idx in range(len(nums) - 1):
            can_reach_idx_element = max_reach >= idx
            if can_reach_idx_element:
                max_reach = max(max_reach, idx + nums[idx])

        return max_reach >= len(nums) - 1
```

## Notes
The first solution I came up with was a simple recursion.
```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        return self.canJumpHelper(nums, 0)

    def canJumpHelper(self, nums: List[int], idx: int) -> bool:
        if idx >= len(nums) - 1:
            return True
        
        for jump in range(1, nums[idx] + 1):
            if self.canJumpHelper(nums, idx + jump):
                return True

        return False
```

Then, I used memoization to have a solution using dynamic programming. This solution has `O(n^2)` time complexity and `O(n)` space complexity.
The idea is that `dp[idx] = True` if we can reach the idx element of the array.
```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        dp = [False] * len(nums)
        dp[0] = True

        for idx in range(1, len(nums)):
            for jdx in range(idx):
                if dp[jdx] and nums[jdx] + jdx >= idx:
                    dp[idx] = True

        return dp[-1]
```

At this point I thought I was done but ouch, I got a Time Limit Exceeded! So, I discovered a very simple solution that uses a greedy approach. The idea is that `max_reach` keeps track of the maximum index we can reach so far. This final solution has `O(n)` time complexity and `O(1)` space complexity.