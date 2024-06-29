## [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)

<h2 style="color:#fac31d">Medium</h2>

Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

## Solution
```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        visited = self.getUnvisitedGrid(grid)
        num_islands = 0

        for row in range(len(grid)):
            for col in range(len(grid[0])):
                num_islands += self.dfs(grid, row, col, visited)
        
        return num_islands
    

    def getUnvisitedGrid(self, grid: List[List[str]]) -> List[List[bool]]:
        unvisited_grid = []
        for _ in range(len(grid)):
            unvisited_row = [False] * len(grid[0])
            unvisited_grid.append(unvisited_row)
        return unvisited_grid


    def dfs(self, grid: List[List[str]], row: int, col: int, visited: List[List[bool]]) -> int:
        if self.outOfGrid(grid, row, col):
            return 0
        if visited[row][col]:
            return 0
        if grid[row][col] == "0":
            return 0
        
        visited[row][col] = True

        self.dfs(grid, row - 1, col, visited)
        self.dfs(grid, row + 1, col, visited)
        self.dfs(grid, row, col - 1, visited)
        self.dfs(grid, row, col + 1, visited)

        return 1


    def outOfGrid(self, grid: List[List[str]], row: int, col: int) -> bool:
        return row < 0 or col < 0 or row >= len(grid) or col >= len(grid[0])
```

## Notes
Perform a depth-first search on the grid on each cell of the grid: every time you find a `"1"`, discover all the other adjacent cells that form an island.

Besides, every time you visit a cell, mark it as visited, in order not to visit an island multiple times.

Every cell is visited at most 5 times: 1 time in the two nested for loops of the main method, and 4 times by the adjacent cells.
So, time complexity of this algorithm is `O(5 * m * n)` = `O(m * n)`.