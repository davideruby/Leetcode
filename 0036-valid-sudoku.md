## [36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku/)

${\textsf{\color{yellow}Medium}}$

Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

- Each row must contain the digits 1-9 without repetition.
- Each column must contain the digits 1-9 without repetition.
- Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.

Note:

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

## Solution
```python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        return (
            self.checkColumns(board) and
            self.checkRows(board) and
            self.checkSubBoxes(board)
        )
        
    def checkRows(self, board: List[List[str]]) -> bool:
        for row in range(9):
            nums = set()
            for col in range(9):
                if board[row][col] in nums and board[row][col] != ".":
                    return False
                nums.add(board[row][col])
        
        return True
    
    def checkColumns(self, board: List[List[str]]) -> bool:
        for col in range(9):
            nums = set()
            for row in range(9):
                if board[row][col] in nums and board[row][col] != ".":
                    return False
                nums.add(board[row][col])
        
        return True

    def checkSubBoxes(self, board: List[List[str]]) -> bool:
        for sub_box_row in range(3):
            for sub_box_col in range(3):
                nums = set()
                for row in range(3):
                    for col in range(3):
                        r = sub_box_row * 3 + row
                        c = sub_box_col * 3 + col
                        if board[r][c] in nums and board[r][c] != ".":
                            return False
                        nums.add(board[r][c])
        
        return True
```
