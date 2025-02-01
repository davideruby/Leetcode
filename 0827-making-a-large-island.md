## [827. Making A Large Island](https://leetcode.com/problems/making-a-large-island/)

${\textsf{\color{red}Hard}}$

You are given an n x n binary matrix grid. You are allowed to change at most one 0 to be 1.

Return the size of the largest island in grid after applying this operation.

An island is a 4-directionally connected group of 1s.

## Solution
```python
class Solution:
    def largestIsland(self, grid: List[List[int]]) -> int:
        num = len(grid)
        sizes = [ [0] * num for _ in range(num)]
        visited = set()
        labels = [ [0] * num for _ in range(num)]
        label = 1

        # 1. Get for each island a label and its size
        for row in range(num):
            for col in range(num):
                if grid[row][col] == 1 and (row, col) not in visited:
                    island_cells = self.dfs(grid, row, col, visited, set())
                    
                    island_size = len(island_cells)
                    for ir, ic in island_cells: # this for does not makes O(n) time complexity higher!
                        sizes[ir][ic] = island_size
                        labels[ir][ic] = label
                    
                    label += 1

        # Manage the edge case when the grid is made by all ones
        num_islands = label - 1 # a little trick to get the number of islands
        all_ones = sizes[0][0] == num * num # when the grid is made by all ones
        if num_islands == 1 and all_ones:
            return num * num

        # 2. Try to connect islands flipping a zero
        max_size = 0
        for row in range(num):
            for col in range(num):
                if grid[row][col] == 0:
                    max_size = max(max_size, self.connectIslands(grid, row, col, labels, sizes))
        
        return max_size


    def dfs(self, grid, row, col, visited, cells):
        if self.outOfBound(grid, row, col) or (row, col) in visited or grid[row][col] == 0:
            return cells
        
        visited.add((row, col))
        cells.add((row, col))
        for nr, nc in [ [row + 1, col], [row - 1, col], [row, col + 1], [row, col - 1] ]:
            self.dfs(grid, nr, nc, visited, cells)
        
        return cells


    def outOfBound(self, grid, row, col):
        return row < 0 or col < 0 or row >= len(grid) or col >= len(grid)


    def connectIslands(self, grid, row, col, labels, sizes):
        connected = set()
        size = 0

        for nr, nc in [ [row + 1, col], [row - 1, col], [row, col + 1], [row, col - 1] ]:
            if not self.outOfBound(grid, nr, nc) and labels[nr][nc] != 0 and labels[nr][nc] not in connected:
                size += sizes[nr][nc]
                connected.add(labels[nr][nc])
        
        return size + 1
```

## Notes
2 steps to success:
1. Try to identify each islands, and assign to each of them a unique label and its size.
2. For each 0-cell, check if it can connect two or more islands and get the total size of the connected islands.
