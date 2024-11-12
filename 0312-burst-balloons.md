## [312. Burst Balloons](https://leetcode.com/problems/burst-balloons/)

${\textsf{\color{red}Hard}}$

You are given n balloons, indexed from 0 to n - 1. Each balloon is painted with a number on it represented by an array nums. You are asked to burst all the balloons.

If you burst the ith balloon, you will get nums[i - 1] * nums[i] * nums[i + 1] coins. If i - 1 or i + 1 goes out of bounds of the array, then treat it as if there is a balloon with a 1 painted on it.

Return the maximum coins you can collect by bursting the balloons wisely.

## Solution
```python
class Solution:
    def maxCoins(self, nums: List[int]) -> int:
        bounded_nums = [1] + nums + [1]
        cache = [ [None] * len(bounded_nums) for _ in range(len(bounded_nums))]
        return self.helper(bounded_nums, 1, len(bounded_nums) - 2, cache)


    def helper(self, nums: List[int], left: int, right: int, cache: List[List[int]]):
        if left > right:
            return 0
        if cache[left][right] is not None:
            return cache[left][right]

        max_coins = 0
        for idx in range(left, right + 1):
            coins = (
                nums[left - 1] * nums[idx] * nums[right + 1] +
                self.helper(nums, left, idx - 1, cache) + 
                self.helper(nums, idx + 1, right, cache)
            )
            max_coins = max(max_coins, coins)
        
        cache[left][right] = max_coins
        return cache[left][right]
```

## Notes
This problem is hard, but I mean ${\textsf{\color{red}hard}}$ ${\textsf{\color{red}hard}}$ ${\textsf{\color{red}hard}}$.

Watch this video: https://www.youtube.com/watch?v=VFskby7lUbw
