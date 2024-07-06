## [130. Surrounded Regions](https://leetcode.com/problems/surrounded-regions/)

<h2 style="color:#fac31d">Medium</h2>
You are given an m x n matrix board containing letters 'X' and 'O', capture regions that are surrounded:

- Connect: A cell is connected to adjacent cells horizontally or vertically.
- Region: To form a region connect every 'O' cell.
- Surround: The region is surrounded with 'X' cells if you can connect the region with 'X' cells and none of the region cells are on the edge of the board.

A surrounded region is captured by replacing all 'O's with 'X's in the input matrix board.

## Solution
```python
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        num_rows = len(board)
        num_cols = len(board[0])
        visited = set()
        for row in range(num_rows):
            self.dfs(board, row, 0, visited)
            self.dfs(board, row, num_cols - 1, visited)

        for col in range(num_cols):
            self.dfs(board, 0, col, visited)
            self.dfs(board, num_rows - 1, col, visited)

        for row in range(num_rows):
            for col in range(num_cols):
                if (row, col) not in visited:
                    board[row][col] = "X"
    

    def dfs(self, board, row, col, visited):
        if row < 0 or col < 0 or row >= len(board) or col >= len(board[0]):
            return
        if board[row][col] == "X":
            return
        if (row, col) in visited:
            return
        
        visited.add((row, col))
        self.dfs(board, row - 1, col, visited)
        self.dfs(board, row + 1, col, visited)
        self.dfs(board, row, col - 1, visited)
        self.dfs(board, row, col + 1, visited)
```

## Notes
Instead of discovering the surrounded regions, try the "reverse" approach.
Start a dfs from the borders of the board to discover the not surrounded regions and then mark with "X" the other regions.
