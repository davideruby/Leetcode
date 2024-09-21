## [1004. Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)

<h2 style="color:#fac31d">Medium</h2>

Given a binary array nums and an integer k, return the maximum number of consecutive 1's in the array if you can flip at most k 0's.

## Solution
```python
class Solution:
    def longestOnes(self, nums: List[int], k: int) -> int:
        longest_ones = 0
        flips = 0
        left = 0

        for right in range(len(nums)):
            if nums[right] == 0:
                flips += 1

            while flips > k:
                if nums[left] == 0:
                    flips -= 1
                left += 1

            longest_ones = max(longest_ones, right - left + 1)

        return longest_ones
```

## Notes
Using a sliding window we can achieve a solution of `O(n)` time complexity. The inner `while` loop can be replaced by an `if`, but I find the solution with the `while` more straightforward.
