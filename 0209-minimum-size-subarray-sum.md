## [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

<h2 style="color:#fac31d">Medium</h2>
Given an array of positive integers nums and a positive integer target, return the minimal length of a 
subarray whose sum is greater than or equal to target. If there is no such subarray, return 0 instead.

## Solution
```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        solution = len(nums) + 1
        found_solution = False

        left = 0
        right = 0
        current_sum = 0

        while right < len(nums):
            current_sum += nums[right]
            right += 1

            while current_sum >= target:
                # here we have a solution
                current_solution = right - left
                if current_solution < solution:
                    found_solution = True
                    # we found a better solution
                    solution = current_solution

                current_sum -= nums[left]
                left += 1

        return solution if found_solution else 0
```

## Notes
Use a sliding window. When we increment right, we update the current sum. If the current sum is gte to the `target`, we check if the current window is the one with minimum size. Then we update left until the current sum is no more valid.
