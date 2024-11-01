## [494. Target Sum](https://leetcode.com/problems/target-sum/)

${\textsf{\color{yellow}Medium}}$

You are given an integer array nums and an integer target.

You want to build an expression out of nums by adding one of the symbols '+' and '-' before each integer in nums and then concatenate all the integers.

- For example, if nums = [2, 1], you can add a '+' before 2 and a '-' before 1 and concatenate them to build the expression "+2-1".

Return the number of different expressions that you can build, which evaluates to target.

## Solution
```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        return self.memo(nums, target, 0, 0, {})


    def memo(self, nums: List[int], target: int, current: int, idx: int, cache: Dict):
        if idx == len(nums):
            return int(current == target)
        if (idx, current) in cache:
            return cache[(idx, current)]

        minus = self.memo(nums, target, current - nums[idx], idx + 1, cache)
        plus = self.memo(nums, target, current + nums[idx], idx + 1, cache)
        
        cache[(idx, current)] = minus + plus
        return minus + plus
```

## Notes
This is a dynamic programming problem. The first solution I came up with was through a simple recursion, where the choices are represented by adding or subtracting the current value to the current sum:

```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        return self.memo(nums, target, 0, 0)


    def memo(self, nums: List[int], target: int, current: int, idx: int):
        if idx == len(nums):
            return int(current == target)

        minus = self.memo(nums, target, current - nums[idx], idx + 1)
        plus = self.memo(nums, target, current + nums[idx], idx + 1)
        
        return minus + plus
```

Then, we have to think how we can enhance this solution with memoization, in order to avoid to do repeated work.
To do that, we have to understand which are the "state variables". In this problem, these state variables are:
- The index: it tells us what values we have considered and what values we haven't considered yet.
- The current sum: it gives us the sum of all the values we have processed so far.
