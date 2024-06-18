## [17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

<h2 style="color:#fac31d">Medium</h2>

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

## Solution
```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        self.telephone = {
            '2': ['a', 'b', 'c'],
            '3': ['d', 'e', 'f'],
            '4': ['g', 'h', 'i'],
            '5': ['j', 'k', 'l'],
            '6': ['m', 'n', 'o'],
            '7': ['p', 'q', 'r', 's'],
            '8': ['t', 'u', 'v'],
            '9': ['w', 'x', 'y', 'z']
        }

        if digits == "":
            return []

        solutions = []
        self.letterCombinationsHelper(digits, 0, "", solutions)
        return solutions


    def letterCombinationsHelper(self, digits: str, idx: int, combination: str, solutions: List[str]) -> None:
        if idx == len(digits):
            solutions.append(combination)
            return
        
        for letter in self.telephone[digits[idx]]:
            combination += letter
            self.letterCombinationsHelper(digits, idx + 1, combination, solutions)
            combination = combination[:len(combination) - 1]

```

## Notes
Perform a backtracking: for each digit, recursively call the backtracking function with the next digit.
