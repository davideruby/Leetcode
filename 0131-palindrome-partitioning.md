## [131. Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/)

<h2 style="color:#fac31d">Medium</h2>

Given a string s, partition s such that every substring of the partition is a palindrome. 
Return all possible palindrome partitioning of s.

## Solution
```python
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        solutions = []
        self.backtracking(s, [], solutions)
        return solutions


    def backtracking(self, s: str, current: List[str], solutions: List[List[str]]) -> None:
        if len(current) > 0 and (not self.isPalindrome(current[-1])):
            # prune
            return
            
        if len(s) == 0:
            solutions.append(current.copy())
            return

        for idx in range(1, len(s) + 1):
            current.append(s[:idx])
            self.backtracking(s[idx:], current, solutions)
            current.pop()

    
    def isPalindrome(self, s: str) -> bool:
        idx = 0
        jdx = len(s) - 1
        while idx <= jdx:
            if s[idx] != s[jdx]:
                return False
            idx += 1
            jdx -= 1
        return True
```

## Notes
How can we generate all the possible partition of the string `s`?
For each `idx` in `range(1, len(s) + 1)`, we take `s[:idx]` as the first element of the partition, and then we take every partition of `s[idx:]`. 
The pruning is done when the last string which has been inserted in the partition is not palindrome.
