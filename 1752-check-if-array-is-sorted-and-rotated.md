## [1752. Check if Array Is Sorted and Rotated](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/)

${\textsf{\color{green}Easy}}$

Given an array nums, return true if the array was originally sorted in non-decreasing order, then rotated some number of positions (including zero). Otherwise, return false.

There may be duplicates in the original array.

Note: An array A rotated by x positions results in an array B of the same length such that A[i] == B[(i+x) % A.length], where % is the modulo operation.

## Solution
```python
class Solution:
    def check(self, nums: List[int]) -> bool:
        irregularities = 0

        for idx in range(len(nums)):
            if nums[idx] > nums[(idx + 1) % len(nums)]:
                irregularities += 1

        return irregularities <= 1
```

## Notes
Even though it's easy to find a solution of this problem, I think that it is not easy to come up with an optimal (that said `O(n)`) solution.
