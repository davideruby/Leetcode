## [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

<h2 style="color:#fac31d">Medium</h2>
There is an integer array nums sorted in ascending order (with distinct values).

Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].

Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.

You must write an algorithm with O(log n) runtime complexity.

## Solution
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1

        while left <= right:
            middle = (left + right) // 2

            if nums[middle] == target:
                return middle
            
            if nums[middle] < nums[right]:
                # right half is ordered
                if nums[middle] < target and target <= nums[right]:
                    left = middle + 1
                else:
                    right = middle - 1
            else:
                # left half is ordered
                if nums[left] <= target and target < nums[middle]:
                    right = middle - 1
                else:
                    left = middle + 1
                    
        return -1
```

## Notes
In my honest opinion, this problem is not real medium. I mean, at first glance the code could be look pretty simple, but actually there are a lot of condition which are not very immediate to understand.

The key of my solution is that I check which half of the array is sorted.
For example, let's suppose the right half is ordered. Then, I check if the target is between middle and right. If so, I move the left pointer, otherwise I move the right one. 
The same reasoning is applied when the left half is ordered.