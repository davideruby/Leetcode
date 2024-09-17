## [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)

<h2 style="color:#ff375f">Hard</h2>

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

## Solution
```python
class Solution:
    # First solution: O(n) time, O(n) space
    def trap(self, height: List[int]) -> int:
        max_left = [0] * len(height)
        max_right = [0] * len(height)

        max_l = 0
        for idx in range(len(height)):
            max_left[idx] = max_l
            if height[idx] > max_l:
                max_l = height[idx]

        max_r = 0
        for idx in range(len(height) - 1, -1, -1):
            max_right[idx] = max_r
            max_r = max(max_r, height[idx])

        water = 0
        for idx in range(len(height)):
            trapped_water = min(max_left[idx], max_right[idx]) - height[idx]
            if trapped_water > 0:
                water += trapped_water

        return water

    # Second solution: O(n) time, O(1) space
    def trap(self, height: List[int]) -> int:
        water = 0
        left = 0
        right = len(height) - 1
        max_left = height[left]
        max_right = height[right]

        while left < right:
            if max_left < max_right:
                trapped_water = min(max_left, max_right) - height[left]
                if trapped_water > 0:
                    water += trapped_water
                left += 1
                if height[left] > max_left:
                    max_left = height[left]
            else:
                trapped_water = min(max_left, max_right) - height[right]
                if trapped_water > 0:
                    water += trapped_water
                right -= 1
                if height[right] > max_right:
                    max_right = height[right]

        return water
```

## Notes
- The first approach to solve the problem is this idea: for each height, we consider the maximum elevation to its left and to its right. Then, the water we can trap over that height is: the minimum between these two values and height itself: `min(max_left, max_right) - height`. If this value is less than 0, discard it.
The values of max_left and max_right can be calculated in O(n) time, using arrays of O(n) space.
- The second approach is the same, but it gets rid of the max_left and max_right arrays. It uses two pointers, left starting from 0 and right starting from the end. max_left and max_right are initialized to height[0] and height[-1]. Since max_left and max_right can only increase during the algorithm and we care about taking the minimum between them, we can get immediately the value `min(max_left, max_right)` and then decrease the current height. I found this solution very hard to understand.
