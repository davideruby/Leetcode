## [10. Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)

${\textsf{\color{red}Hard}}$

Given an input string s and a pattern p, implement regular expression matching with support for '.' and '*' where:

- '.' Matches any single character.​​​​
- '*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

## Solution
```python
# O(n*m) time, O(m) space
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        prev_row = [False] * (len(p) + 1)
        prev_row[-1] = True
        for idx2 in range(len(p) - 2, -1, -1):
            if p[idx2 + 1] == "*":
                prev_row[idx2] = prev_row[idx2 + 2]

        for idx1 in range(len(s) - 1, -1, -1):
            cur_row = [False] * (len(p) + 1)

            for idx2 in range(len(p) - 1, -1, -1):
                match_current_char = (s[idx1] == p[idx2] or p[idx2] == ".")
                
                if idx2 < len(p) - 1 and p[idx2 + 1] == "*":
                    cur_row[idx2] = (
                        cur_row[idx2 + 2] or 
                        (match_current_char and prev_row[idx2])
                    )
                elif match_current_char:
                    cur_row[idx2] = prev_row[idx2 + 1]

            prev_row = cur_row

        return prev_row[0]
```

## Notes
This is a very hard dynamic programming problem. If you came up with a solution by yourself, my congrats. It is very hard to get to the solution due to the edge cases in my opinion.

Anyway, the brute-force recursive solution is the following:
```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        return self.helper(s, p, 0, 0)

    def helper(self, s: str, p: str, idx1: int, idx2: int):
        if idx1 >= len(s) and idx2 >= len(p):
            return True
        if idx2 >= len(p):
            return False

        match_current_char = idx1 < len(s) and (s[idx1] == p[idx2] or p[idx2] == ".")
        is_match = False
        if idx2 < len(p) - 1 and p[idx2 + 1] == "*":
            is_match = (self.helper(s, p, idx1, idx2 + 2) or
                    (match_current_char and self.helper(s, p, idx1 + 1, idx2)))
        elif match_current_char:
            is_match = self.helper(s, p, idx1 + 1, idx2 + 1)

        return is_match
```

When the current characters of `p` and `s` match or the character of `p` is `"."`, the solution is trivial. The difficulty of this problem consists of dealing with the `*`. These lines handle the `*`:
```python
if idx2 < len(p) - 1 and p[idx2 + 1] == "*":
    is_match = (self.helper(s, p, idx1, idx2 + 2) or
            (match_current_char and self.helper(s, p, idx1 + 1, idx2)))
```
Here we are saying, if the next character of `p` is a `*`, then we can either:
- not to use the `*`, so jump to two characters forward of `p`: `self.helper(s, p, idx1, idx2 + 2)`, or:
- use the `*`, so the current character of `s` and `p` must match and then we jump to the next character of `s`: `match_current_char and self.helper(s, p, idx1 + 1, idx2)`

Then, we can memoize this solution to have a dynamic programming top-down solution:
```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        cache = [ [None] * (len(p) + 1) for _ in range(len(s) + 1)]
        return self.helper(s, p, 0, 0)

    def helper(self, s: str, p: str, idx1: int, idx2: int, cache):
        if idx1 >= len(s) and idx2 >= len(p):
            return True
        if idx2 >= len(p):
            return False
        if cache[idx1][idx2] is not None:
            return cache[idx1][idx2]

        match_current_char = idx1 < len(s) and (s[idx1] == p[idx2] or p[idx2] == ".")
        is_match = False
        if idx2 < len(p) - 1 and p[idx2 + 1] == "*":
            is_match = (self.helper(s, p, idx1, idx2 + 2, cache) or
                    (match_current_char and self.helper(s, p, idx1 + 1, idx2, cache)))
        elif match_current_char:
            is_match = self.helper(s, p, idx1 + 1, idx2 + 1, cache)

        cache[idx1][idx2] = is_match
        return is_match
```

Now, we can turn it into the iterative bottom-up version:
```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        cache = [ [False] * (len(p) + 1) for _ in range(len(s) + 1)]
        cache[-1][-1] = True

        for idx2 in range(len(p) - 2, -1, -1):
            if p[idx2 + 1] == "*":
                cache[-1][idx2] = cache[-1][idx2 + 2]

        for idx1 in range(len(s) - 1, -1, -1):
            for idx2 in range(len(p) - 1, -1, -1):
                match_current_char = (s[idx1] == p[idx2] or p[idx2] == ".")
                
                if idx2 < len(p) - 1 and p[idx2 + 1] == "*":
                    cache[idx1][idx2] = (
                        cache[idx1][idx2 + 2] or 
                        (match_current_char and cache[idx1 + 1][idx2])
                    )
                elif match_current_char:
                    cache[idx1][idx2] = cache[idx1 + 1][idx2 + 1]

        return cache[0][0]
```
Note that we add an extra row and an extra column to our `cache`: the last column is for `p = ""` and last row is for `s = ""`.
Finally, you can notice that to compute the row, we just need the previous one. So we can optimize this solution to have just `O(m)` space complexity.