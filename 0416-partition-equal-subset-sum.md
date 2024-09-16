## [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)

<h2 style="color:#fac31d">Medium</h2>

Given an integer array nums, return true if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or false otherwise.

## Solution
```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        if sum(nums) % 2 == 1:
            return False

        target = sum(nums) / 2
        dp = set([0])

        for num in nums:
            
            sums = set()
            for previous_sum in dp:
                new_sum = previous_sum + num
                if new_sum == target:
                    return True
                sums.add(new_sum)

            dp = dp.union(sums)  

        return False
```

## Notes
The key insight is that if the array can be partitioned, the two subset sums must be the total sum divided by 2.
So, we have to find a subset of the array whose sum is `sum(nums) / 2`.

Basically, we use dynamic programming to generate every subset sum and we return `True` as soon as we find our target. 