## [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

<h2 style="color:#00b8a3">Easy</h2>
Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.

Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:

- Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
- Return k.

## Solution
```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        left = 0

        for right in range(len(nums)):
            if nums[right] != nums[left]:
                left += 1
                nums[left] = nums[right]

        return left + 1
```

## Notes
Use two pointers which start from the beginning. The right pointer loops over the array. At each iteration check if `arr[left] != arr[right]`. If so, increase the left pointer and copy the element at right position. At the end, return `left + 1`.
