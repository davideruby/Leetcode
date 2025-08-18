## [463. Island Perimeter](https://leetcode.com/problems/island-perimeter/)

${\textsf{\color{green}Easy}}$

You are given row x col grid representing a map where grid[i][j] = 1 represents land and grid[i][j] = 0 represents water.

Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells).

The island doesn't have "lakes", meaning the water inside isn't connected to the water around the island. One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.

## Solution
```python
class Solution:
    def islandPerimeter(self, grid: List[List[int]]) -> int:
        visited = set()
        WATER = 0
        LAND = 1

        def dfs(row, col):
            if row < 0 or col < 0 or row >= len(grid) or col >= len(grid[0]):
                return 1

            if grid[row][col] == WATER:
                return 1

            if (row, col) in visited:
                return 0

            visited.add((row, col))

            return (
                dfs(row - 1, col) + 
                dfs(row + 1, col) + 
                dfs(row, col - 1) +
                dfs(row, col + 1)
            )

        for row in range(len(grid)):
            for col in range(len(grid[0])):
                if grid[row][col] == LAND:
                    return dfs(row, col)
```

## Notes
Get the perimeter through a depth-first search.
