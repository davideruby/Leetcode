## [2658. Maximum Number of Fish in a Grid](https://leetcode.com/problems/maximum-number-of-fish-in-a-grid/)

${\textsf{\color{yellow}Medium}}$

You are given a 0-indexed 2D matrix grid of size m x n, where (r, c) represents:

- A land cell if grid[r][c] = 0, or
- A water cell containing grid[r][c] fish, if grid[r][c] > 0.

A fisher can start at any water cell (r, c) and can do the following operations any number of times:

- Catch all the fish at cell (r, c), or
- Move to any adjacent water cell.

Return the maximum number of fish the fisher can catch if he chooses his starting cell optimally, or 0 if no water cell exists.

An adjacent cell of the cell (r, c), is one of the cells (r, c + 1), (r, c - 1), (r + 1, c) or (r - 1, c) if it exists.

## Solution
```python
class Solution:
    def findMaxFish(self, grid: List[List[int]]) -> int:
        max_fish = 0
        visited = set()

        for row in range(len(grid)):
            for col in range(len(grid[row])):
                max_fish = max(max_fish, self.dfs(grid, row, col, visited))

        return max_fish

    
    def dfs(self, grid, row, col, visited):
        if row < 0 or col < 0 or row >= len(grid) or col >= len(grid[0]):
            return 0
        if grid[row][col] == 0:
            return 0
        if (row, col) in visited:
            return 0

        visited.add((row, col))
        fish = grid[row][col]
        for dr, dc in [ [-1, 0], [1, 0], [0, -1], [0, 1] ]:
            fish += self.dfs(grid, row + dr, col + dc, visited)

        return fish
```

## Notes
A DFS of the grid.
