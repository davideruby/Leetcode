## [1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)

${\textsf{\color{yellow}Medium}}$

Given two strings text1 and text2, return the length of their longest common subsequence. If there is no common subsequence, return 0.

A subsequence of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

- For example, "ace" is a subsequence of "abcde".

A common subsequence of two strings is a subsequence that is common to both strings.

## Solution
```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        cache = [ [0] * (len(text2) + 1) for _ in range(len(text1) + 1)]
        
        for idx1 in range(len(text1) - 1, -1, -1):
            for idx2 in range(len(text2) - 1, -1, -1):
                if text1[idx1] == text2[idx2]:
                    cache[idx1][idx2] = 1 + cache[idx1 + 1][idx2 + 1]
                else:
                    cache[idx1][idx2] = max(cache[idx1 + 1][idx2], cache[idx1][idx2 + 1])
        
        return cache[0][0]
```

## Notes
This is one the dynamic programming problem you should study more than solve.

First, we have the recurisve brute-force solution, with time complexity `O(2^(n + m))`:
```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        return self.helper(text1, text2, 0, 0)

    def helper(self, text1: str, text2: str, idx1: int, idx2: int):
        if idx1 == len(text1) or idx2 == len(text2):
            return 0

        if text1[idx1] == text2[idx2]:
            return 1 + self.helper(text1, text2, idx1 + 1, idx2 + 1)

        lcs1 = self.helper(text1, text2, idx1 + 1, idx2)
        lcs2 = self.helper(text1, text2, idx1, idx2 + 1)
        return max(lcs1, lcs2)
```

Then, we can memoize this solution to avoid repeated work:
```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        cache = [ [-1] * len(text2) for _ in range(len(text1))]
        return self.helper(text1, text2, 0, 0, cache)

    def helper(self, text1: str, text2: str, idx1: int, idx2: int, cache: List[List[int]]):
        if idx1 == len(text1) or idx2 == len(text2):
            return 0

        if cache[idx1][idx2] != -1:
            return cache[idx1][idx2]

        if text1[idx1] == text2[idx2]:
            cache[idx1][idx2] = 1 + self.helper(text1, text2, idx1 + 1, idx2 + 1, cache)
        else:
            lcs1 = self.helper(text1, text2, idx1 + 1, idx2, cache)
            lcs2 = self.helper(text1, text2, idx1, idx2 + 1, cache)
            cache[idx1][idx2] = max(lcs1, lcs2)

        return cache[idx1][idx2]
```

Finally, we can turn this version in the iterative bottom-up one.