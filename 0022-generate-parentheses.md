## [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

<h2 style="color:#fac31d">Medium</h2>
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

## Solution
```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        result = []
        self.generateParenthesisHelper(n, 0, 0, "", result)
        return result

    def generateParenthesisHelper(self, n: int, nOpen: int, nClose: int, currentString: str, result: List[str]):
        if nOpen == nClose == n:
            result.append(currentString)

        if nOpen < n:
            self.generateParenthesisHelper(n, nOpen + 1, nClose, f"{currentString}(", result)
        if nClose < nOpen:
            self.generateParenthesisHelper(n, nOpen, nClose + 1, f"{currentString})", result)
```

## Notes
Use recursion and keep track of how many opening and closing parenthesis you have. If you can still add an opening parenthesis, call the backtracking function with an additional opening parenthesis. Same with a closing parenthesis when you have that closing parenthesis are less than opening ones. Return the result when `nOpen == nClose == n`
