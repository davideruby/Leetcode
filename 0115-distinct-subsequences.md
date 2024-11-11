## [115. Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/)

${\textsf{\color{red}Hard}}$

Given two strings s and t, return the number of distinct subsequences of s which equals t.

The test cases are generated so that the answer fits on a 32-bit signed integer.

## Solution
```python
class Solution:
    def numDistinct(self, s: str, t: str) -> int:
        cache = [ [0] * (len(t) + 1) for _ in range(len(s) + 1)]
        for idx in range(len(s) + 1):
            cache[idx][-1] = 1

        for idx_t in range(len(t) - 1, -1, -1):
            for idx_s in range(len(s) - 1, -1, -1):
                cache[idx_s][idx_t] = cache[idx_s + 1][idx_t]
                if s[idx_s] == t[idx_t]:
                    cache[idx_s][idx_t] += cache[idx_s + 1][idx_t + 1]

        return cache[0][0]
```

## Notes
This is a dynamic programming problem, very similar to the [Longest Common Subsequence (LCS)](./1143-longest-common-subsequence.md).

Brute-force recursive solution:
```python
class Solution:
    def numDistinct(self, s: str, t: str) -> int:
        return self.helper(s, t, 0, 0)

    def helper(self, s, t, idx1, idx2):
        if idx2 == len(t):
            return 1
        
        if idx1 == len(s):
            return 0

        num_sequence = self.helper(s, t, idx1 + 1, idx2)
        if s[idx1] == t[idx2]:
            num_sequence += self.helper(s, t, idx1 + 1, idx2 + 1)
        
        return num_sequence 
```

Let's memoize the solution:
```python
class Solution:
    def numDistinct(self, s: str, t: str) -> int:
        cache = [ [None] * len(t) for _ in range(len(s))]
        return self.helper(s, t, 0, 0, cache)

    def helper(self, s, t, idx1, idx2, cache):
        if idx2 == len(t):
            return 1
        
        if idx1 == len(s):
            return 0

        if cache[idx1][idx2] is not None:
            return cache[idx1][idx2]

        num_sequence = self.helper(s, t, idx1 + 1, idx2, cache)
        if s[idx1] == t[idx2]:
            num_sequence += self.helper(s, t, idx1 + 1, idx2 + 1, cache)
        
        cache[idx1][idx2] = num_sequence
        return num_sequence
```

And finally, let's turn this solution into the bottom-up iterative version.