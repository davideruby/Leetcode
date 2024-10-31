## [724. Find Pivot Index](https://leetcode.com/problems/find-pivot-index/)

${\textsf{\color{green}Easy}}$

Given an array of integers nums, calculate the pivot index of this array.

The pivot index is the index where the sum of all the numbers strictly to the left of the index is equal to the sum of all the numbers strictly to the index's right.

If the index is on the left edge of the array, then the left sum is 0 because there are no elements to the left. This also applies to the right edge of the array.

Return the leftmost pivot index. If no such index exists, return -1.

## Solution
```python
class Solution:
    def pivotIndex(self, nums: List[int]) -> int:
        right_sum = sum(nums)
        left_sum = 0

        for idx, num in enumerate(nums):
            right_sum -= num
            
            if left_sum == right_sum:
                return idx

            left_sum += num

        return -1
```

## Notes
As we iterate through the array of numbers, keep track of the sum of the values on the current number's left and its right.
