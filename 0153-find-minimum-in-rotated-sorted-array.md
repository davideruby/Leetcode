## [153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

<h2 style="color:#fac31d">Medium</h2>
Suppose an array of length n sorted in ascending order is rotated between 1 and n times. For example, the array nums = [0,1,2,4,5,6,7] might become:

- [4,5,6,7,0,1,2] if it was rotated 4 times.
- [0,1,2,4,5,6,7] if it was rotated 7 times.

Notice that rotating an array [a[0], a[1], a[2], ..., a[n-1]] 1 time results in the array [a[n-1], a[0], a[1], a[2], ..., a[n-2]].

Given the sorted rotated array nums of unique elements, return the minimum element of this array.

You must write an algorithm that runs in O(log n) time.

## Solution
```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        left = 0
        right = len(nums) - 1
        min_num = nums[0]

        while left <= right:
            middle = (left + right) // 2

            if nums[middle] < min_num:
                min_num = nums[middle]

            if nums[middle] > nums[right]:
                left = middle + 1
            else:
                right = middle - 1
        
        return min_num
```

## Notes
Of course, the solution is achieved with a binary search. The key is that if `nums[middle] > nums[right]`, it means that somewhere between middle and right we have `..., a[n - 1], a[0], ...,` where a[0] is the minimum number. Otherwise search the minimum in the left half.