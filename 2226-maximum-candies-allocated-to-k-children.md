## [2226. Maximum Candies Allocated to K Children](https://leetcode.com/problems/maximum-candies-allocated-to-k-children/)

${\textsf{\color{yellow}Medium}}$

You are given a 0-indexed integer array candies. Each element in the array denotes a pile of candies of size candies[i]. You can divide each pile into any number of sub piles, but you cannot merge two piles together.

You are also given an integer k. You should allocate piles of candies to k children such that each child gets the same number of candies. Each child can be allocated candies from only one pile of candies and some piles of candies may go unused.

Return the maximum number of candies each child can get.

## Solution
```python
class Solution:
    def maximumCandies(self, candies: List[int], k: int) -> int:
        left = 1
        right = max(candies)
        res = 0

        while left <= right:
            num_candies = (left + right) // 2

            if self.canGiveNumCandies(candies, k, num_candies):
                res = num_candies
                left = num_candies + 1
            else:
                right = num_candies - 1
        
        return res

    def canGiveNumCandies(self, candies, num_children, num_candies):
        satisfied = 0

        for candy in candies:
            satisfied += candy // num_candies
            if satisfied >= num_children:
                return True
        
        return False
```

## Notes
Use a binary search to get the maximum number of candies we can give to each children.