## [417. Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/)

<h2 style="color:#fac31d">Medium</h2>

Problem description

## Solution
```python
from collections import deque

class Solution:
    def pacificAtlantic(self, heights: List[List[int]]) -> List[List[int]]:
        pacific = set()
        atlantic = set()
        num_rows = len(heights)
        num_cols = len(heights[0])

        for row in range(num_rows):
            self.dfs(heights, row, 0, heights[row][0], pacific)
            self.dfs(heights, row, num_cols - 1, heights[row][num_cols - 1], atlantic)

        for col in range(num_cols):
            self.dfs(heights, 0, col, heights[0][col], pacific)
            self.dfs(heights, num_rows - 1, col, heights[num_rows - 1][col], atlantic)

        return pacific.intersection(atlantic)


    def dfs(self, heights, row, col, prev, visited):
        if row < 0 or col < 0 or row >= len(heights) or col >= len(heights[0]):
            return
        if prev > heights[row][col]:
            return
        if (row, col) in visited:
            return

        visited.add((row, col))
        self.dfs(heights, row - 1, col, heights[row][col], visited)
        self.dfs(heights, row + 1, col, heights[row][col], visited)
        self.dfs(heights, row, col - 1, heights[row][col], visited)
        self.dfs(heights, row, col + 1, heights[row][col], visited)
```

## Notes
In the first solution I implemented, I performed a depth-first search for each cell, checking if the cell could reach both atlantic and pacific coasts. That solution had time complexity `O( (nm)^2 )`.

Then, I noticed (through other's Leetcode solutions) that we can start the depth first search from the end, that said from the Atlantic and pacific coasts. This solution is better because has complexity `O(nm)`.