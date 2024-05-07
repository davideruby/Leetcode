## [84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)

<h2 style="color:#ff375f">Hard</h2>
Given an array of integers heights representing the histogram's bar height where the width of each bar is 1, return the area of the largest rectangle in the histogram.

## Solution
```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        stack = []
        max_area = 0

        for idx, current_height in enumerate(heights + [0]):
            start_area = idx
            while len(stack) > 0 and current_height < stack[-1][0]:
                [height, start] = stack.pop()
                width = idx - start
                area = width * height
                if area > max_area:
                    max_area = area
                start_area = start

            stack.append([current_height, start_area])

        return max_area
```

## Notes
For each element, we have to store in a monotonic stack the height and the index where its area starts. Before pushing into the stack, pop the stack as long as the current height is lower than the height at the top of the stack. Then, calculate the area of the popped element: the height is popped from the stack, and the width is calculated by `current_index - popped_index`. The start index of the current element, instead, is the current_index if no element got popped from the stack, otherwise the start_index of the last popped element. Consider why we pushed in the original `heights` array a final `0`.
