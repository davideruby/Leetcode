## [695. Max Area of Island](https://leetcode.com/problems/max-area-of-island/)

<h2 style="color:#fac31d">Medium</h2>
You are given an m x n binary matrix grid. An island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

The area of an island is the number of cells with a value 1 in the island.

Return the maximum area of an island in grid. If there is no island, return 0.

## Solution
```python
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        visited = self.getUnvisitedGrid(grid)
        max_island_size = 0

        for row in range(len(grid)):
            for col in range(len(grid[0])):
                max_island_size = max(max_island_size, self.dfs(grid, row, col, visited)) 
        
        return max_island_size
        

    def getUnvisitedGrid(self, grid: List[List[int]]) -> List[List[bool]]:
        unvisited_grid = []
        for _ in range(len(grid)):
            unvisited_row = [False] * len(grid[0])
            unvisited_grid.append(unvisited_row)
        return unvisited_grid


    def dfs(self, grid: List[List[int]], row: int, col: int, visited: List[List[bool]]) -> int:
        if self.outOfGrid(grid, row, col):
            return 0
        if grid[row][col] == 0:
            return 0
        if visited[row][col]:
            return 0

        visited[row][col] = True
        island_size = 1
        island_size += self.dfs(grid, row - 1, col, visited)
        island_size += self.dfs(grid, row + 1, col, visited)
        island_size += self.dfs(grid, row, col - 1, visited)
        island_size += self.dfs(grid, row, col + 1, visited)
        return island_size


    def outOfGrid(self, grid: List[List[int]], row: int, col: int) -> bool:
        return row < 0 or col < 0 or row >= len(grid) or col >= len(grid[0])
```

## Notes
Perform a depth-first search on each cell of the grid: every time you find a `1`, discover all the other adjacent cells to get the area of the island.

Besides, every time you visit a cell, mark it as visited, in order not to visit an island multiple times.

