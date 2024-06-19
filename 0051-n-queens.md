## [51. N-Queens](https://leetcode.com/problems/n-queens/)

<h2 style="color:#ff375f">Hard</h2>

The n-queens puzzle is the problem of placing n queens on an n x n chessboard such that no two queens attack each other.

Given an integer n, return all distinct solutions to the n-queens puzzle. You may return the answer in any order.

Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space, respectively.

## Solution
```python
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        current = [idx for idx in range(n)]
        solutions = []
        self.backtracking(n, 0, current, solutions)
        return self.encodeSolutions(solutions, n)


    def backtracking(self, n: int, idx: int, current: List[int], solutions: List[List[int]]) -> None:
        if not self.isValid(current, idx):
            return
        if idx == n:
            solutions.append(current.copy())
            return

        for jdx in range(idx, n):
            current[jdx], current[idx] = current[idx], current[jdx]
            self.backtracking(n, idx + 1, current, solutions)
            current[jdx], current[idx] = current[idx], current[jdx]


    def isValid(self, current: List[int], idx: int):
        for jdx in range(idx - 1):
            if abs(jdx - (idx - 1)) == abs(current[jdx] - current[idx - 1]):
                return False
        return True


    def encodeSolutions(self, solutions: List[List[int]], n: int) -> List[List[str]]:
        encoded_solutions = []

        for sol in solutions:

            encoded_sol = []
            for queen_idx in sol:
                encoded_row = ["."] * n
                encoded_row[queen_idx] = "Q"
                encoded_sol.append(''.join(encoded_row))
                
            encoded_solutions.append(encoded_sol)

        return encoded_solutions
```

## Notes
In my opinion, the most important thing in this problem is how you represent the solution.
I used an array of length `n`: the element `array[i]` says that the queen `i` stays in row `i` and column `array[i]`.
In addition, the array is initialized as `[0, 1, ..., n - 1]` and in our backtracking method we calculate every permutation of such array.
With this representation, we can't have two queens in the same row (the row is given by the index), nor two queens in the same column (every element in the array is unique). 
The only check we have to do is that two queens can't stay in the same diagonal:
- given two queens q1 in position `(i, array[i])`, and q2 in `(j, array[j])`,
- they are in the same diagonal if `Δy / Δx = 1` or `Δy / Δx = -1` --> `|Δy| = |Δx|` --> `|array[i] - array[j]| = |i - j|`.
