## [45. Jump Game II](https://leetcode.com/problems/jump-game-ii/)

<h2 style="color:#fac31d">Medium</h2>

You are given a 0-indexed array of integers nums of length n. You are initially positioned at nums[0].

Each element nums[i] represents the maximum length of a forward jump from index i. In other words, if you are at nums[i], you can jump to any nums[i + j] where:

- 0 <= j <= nums[i] and
- i + j < n

Return the minimum number of jumps to reach nums[n - 1]. The test cases are generated such that you can reach nums[n - 1].

## Solution
```python
class Solution:
    def jump(self, nums: List[int]) -> int:
        jumps = 0
        max_reach = 0
        farthest = 0

        for idx in range(len(nums) - 1):
            max_reach = max(max_reach, idx + nums[idx])
            if idx == farthest:
                farthest = max_reach
                jumps += 1
        
        return jumps
```

## Notes
This solution uses a greedy approach and has `O(n)` time complexity and `O(1)` space complexity. I think it is simpler to explain the solution directly with an example.

Let's say we have `nums = [2, 3, 1, 1, 4, 5]`.

- We start from `nums[0] = 2`. That means we can get to `nums[1]` or `nums[2]` with 1 jump. 
- So, we have to determine the best element between `nums[1]` and `nums[2]` from where we have to take the next jump. 
- From `nums[1]` we can get to `nums[4]` and from `nums[2]` we can get to `nums[3]`, so the best element is `nums[1]`. 
- Now, we increase the number of performed jumps and again we have to choose which is the best next element between `nums[2]` and `nums[4]`. That element is `nums[4]`: we increase the number of jumps and then we get to the solution.


Initially, I came up with a solution using dynamic programming, which has `O(n^2)` time complexity and `O(n)` space complexity. The idea is that `dp[idx]` stores the minimum number of jumps to store the `idx` element.

```python
class Solution:
    def jump(self, nums: List[int]) -> int:
        dp = [float("inf")] * len(nums)
        dp[0] = 0

        for idx in range(1, len(nums)):
            for jdx in range(idx):
                if jdx + nums[jdx] >= idx:
                    dp[idx] = min(dp[idx], 1 + dp[jdx])
        
        return dp[-1]
```