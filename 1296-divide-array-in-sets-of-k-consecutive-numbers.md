## [1296. Divide Array in Sets of K Consecutive Numbers](https://leetcode.com/problems/divide-array-in-sets-of-k-consecutive-numbers/)

<h2 style="color:#fac31d">Medium</h2>

Given an array of integers nums and a positive integer k, check whether it is possible to divide this array into sets of k consecutive numbers.

Return true if it is possible. Otherwise, return false.

## Solution
```python
from collections import Counter

class Solution:
    def isPossibleDivide(self, nums: List[int], k: int) -> bool:
        counts = Counter(nums)
        nums.sort()

        for num in nums:
            if counts[num] > 0 and not self.canFormGroup(num, nums, k, counts):
                return False
        
        return True

    def canFormGroup(self, num: int, nums: List[int], k: int, counts: Dict[int, int]):
        for group_num in range(num, num + k):
            if counts.get(group_num, 0) == 0:
                return False
            
            counts[group_num] -= 1
        
        return True
```

## Notes
The problem is the same as [846. Hand of Straights](./0846-hand-of-straights.md), so read that solution.
This solution is a variant where we do not use a heap, but we sort the array. The time complexity is again `O(n * logn)`.
