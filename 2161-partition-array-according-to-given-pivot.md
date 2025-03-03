## [2161. Partition Array According to Given Pivot](https://leetcode.com/problems/partition-array-according-to-given-pivot/)

${\textsf{\color{yellow}Medium}}$

You are given a 0-indexed integer array nums and an integer pivot. Rearrange nums such that the following conditions are satisfied:

- Every element less than pivot appears before every element greater than pivot.
- Every element equal to pivot appears in between the elements less than and greater than pivot.
- The relative order of the elements less than pivot and the elements greater than pivot is maintained.
    - More formally, consider every pi, pj where pi is the new position of the ith element and pj is the new position of the jth element. If i < j and both elements are smaller (or larger) than pivot, then pi < pj.
Return nums after the rearrangement.

## Solution
```python
class Solution:
    def pivotArray(self, nums: List[int], pivot: int) -> List[int]:
        pivotted = [pivot] * len(nums)

        idx_less = 0
        for num in nums:
            if num < pivot:
                pivotted[idx_less] = num
                idx_less += 1

        idx_greater = len(nums) - 1
        for num in reversed(nums):
            if num > pivot:
                pivotted[idx_greater] = num
                idx_greater -= 1
        
        return pivotted
```
