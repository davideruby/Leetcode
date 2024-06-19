## [79. Word Search](https://leetcode.com/problems/word-search/)

<h2 style="color:#fac31d">Medium</h2>

Given an m x n grid of characters board and a string word, return true if word exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

## Solution
```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        for row in range(len(board)):
            for col in range(len(board[row])):
                visited = self.getFalseVisitedBoard(board)
                if self.search(board, word, row, col, 0, visited):
                    return True
        
        return False


    def getFalseVisitedBoard(self, board: List[List[int]]) -> List[List[bool]]:
        visited = []
        for row in board:
            visited.append([False] * len(row))
        return visited


    def search(self, board: List[List[str]], word: str, row: int, col: int, idx_word: int, visited: List[List[bool]]) -> bool:
        if idx_word == len(word):
            return True
        
        if self.outOfBoard(board, row, col):
            return False
        if visited[row][col]:
            return False
        if word[idx_word] != board[row][col]:
            return False

        visited[row][col] = True
        if self.search(board, word, row - 1, col, idx_word + 1, visited): # up
            return True
        if self.search(board, word, row + 1, col, idx_word + 1, visited): # down
            return True
        if self.search(board, word, row, col - 1, idx_word + 1, visited): # left
            return True
        if self.search(board, word, row, col + 1, idx_word + 1, visited): # right
            return True

        visited[row][col] = False
        return False


    def outOfBoard(self, board: List[List[int]], row: int, col: int):
        return row < 0 or row >= len(board) or col < 0 or col >= len(board[0])
```

## Notes
Use DFS with 4 directions to search for the word.
