## [219. Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii/)

<h2 style="color:#00b8a3">Easy</h2>

Given an integer array nums and an integer k, return true if there are two distinct indices i and j in the array such that nums[i] == nums[j] and abs(i - j) <= k.

## Solution
```python
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        window_set = set()

        for idx in range(len(nums)):
            if len(window_set) > k:
                window_set.remove(nums[idx - k - 1])
            if nums[idx] in window_set:
                return True
            window_set.add(nums[idx])

        return False
```

## Notes
We use a hashset to keep track of the elements contained in the current window of length `k`.
