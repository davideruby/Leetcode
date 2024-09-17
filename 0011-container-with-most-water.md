## [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

<h2 style="color:#fac31d">Medium</h2>
You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

## Solution
```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        max_area = 0
        idx = 0
        jdx = len(height) - 1

        while idx < jdx:
            container_height = min(height[idx], height[jdx])
            container_width = jdx - idx
            area = container_width * container_height
            if area > max_area:
                max_area = area

            if height[idx] < height[jdx]:
                idx += 1
            elif height[idx] > height[jdx]:
                jdx -= 1
            else:
                idx += 1
                jdx -= 1

        return max_area
```

## Notes
Use two pointers left and right. Left starts from 0 and right from the end of the array. Determine the water which can be contained between left and right lines. Then, move the index related to the minimum line.