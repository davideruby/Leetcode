## [198. House Robber](https://leetcode.com/problems/house-robber/)

<h2 style="color:#fac31d">Medium</h2>

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

## Solution

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        rob1 = 0
        rob2 = 0

        for num in nums:
            tmp = max(rob1 + num, rob2)
            rob1 = rob2
            rob2 = tmp

        return rob2
```

## Notes

The best advice I can give you is to read this guide: https://leetcode.com/problems/house-robber/solutions/156523/from-good-to-great-how-to-approach-most-of-dp-problems
