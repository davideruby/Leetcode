## [2684. Maximum Number of Moves in a Grid](https://leetcode.com/problems/maximum-number-of-moves-in-a-grid/)

${\textsf{\color{yellow}Medium}}$

You are given a 0-indexed m x n matrix grid consisting of positive integers.

You can start at any cell in the first column of the matrix, and traverse the grid in the following way:

- From a cell (row, col), you can move to any of the cells: (row - 1, col + 1), (row, col + 1) and (row + 1, col + 1) such that the value of the cell you move to, should be strictly bigger than the value of the current cell.

Return the maximum number of moves that you can perform.

## Solution
```python
class Solution:
    def maxMoves(self, grid: List[List[int]]) -> int:
        max_moves = 0
        cache = [[-1] * len(grid[0]) for _ in range(len(grid))]
        for row in range(len(grid)):
            max_moves = max(max_moves, self.memo(grid, row, 0, cache))

        return max_moves


    def memo(self, grid: List[List[int]], row: int, col: int, cache: List[List[int]]) -> int:
        if cache[row][col] != -1:
            return cache[row][col]

        moves = 0
        for next_row, next_col in [[row - 1, col + 1], [row, col + 1], [row + 1, col + 1]]:
            if (next_row >= 0 and
                next_row < len(grid) and
                next_col < len(grid[0]) and 
                grid[next_row][next_col] > grid[row][col]):
                moves = max(moves, 1 + self.memo(grid, next_row, next_col, cache))
    
        cache[row][col] = moves
        return moves
```

## Notes
This solution combines recursion and memoization to avoid redundant calculations by caching previously computed values in a `cache` table.
