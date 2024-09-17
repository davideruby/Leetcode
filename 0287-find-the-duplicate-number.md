## [287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)

<h2 style="color:#fac31d">Medium</h2>

Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive.

There is only one repeated number in nums, return this repeated number.

You must solve the problem without modifying the array nums and uses only constant extra space.

## Solution
```python
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        fast = nums[0]
        slow = nums[0]
        while True:
            slow = nums[slow]
            fast = nums[nums[fast]]
            if slow == fast:
                break

        slow2 = nums[0]
        while slow != slow2:
            slow = nums[slow]
            slow2 = nums[slow2]

        return slow2
```

## Notes
Slow and Fast Pointers (Floyd's tortoise and hare algorithm). Think the array of numbers as a list where the element at position `i` has as next element `nums[i]`.
