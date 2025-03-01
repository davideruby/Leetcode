## [1092. Shortest Common Supersequence](https://leetcode.com/problems/shortest-common-supersequence/)

${\textsf{\color{red}Hard}}$

Given two strings str1 and str2, return the shortest string that has both str1 and str2 as subsequences. If there are multiple valid strings, return any of them.

A string s is a subsequence of string t if deleting some number of characters from t (possibly 0) results in the string s.

## Solution
```python
class Solution:
    def shortestCommonSupersequence(self, str1: str, str2: str) -> str:
        prev = [ str2[idx2:] for idx2 in range(len(str2) + 1)]
        
        for idx1 in range(len(str1) - 1, -1, -1):
            curr = [""] * (len(str2) + 1)
            curr[-1] = str1[idx1:]

            for idx2 in range(len(str2) - 1, -1, -1):
                if str1[idx1] == str2[idx2]:
                    curr[idx2] = str1[idx1] + prev[idx2 + 1]
                else:
                    res1 = str1[idx1] + prev[idx2]
                    res2 = str2[idx2] + curr[idx2 + 1]
                    curr[idx2] = res1 if len(res1) < len(res2) else res2
            
            prev = curr

        return prev[0]
```

## Notes
This problem is very similar to the "longest common subsequence" problem, but it is harder due to the space complexity. Let's try to figure this problem out step-by-step.

At first, we code a recursive brute-force solution:
```python
class Solution:
    def shortestCommonSupersequence(self, str1: str, str2: str) -> str:
        return self.helper(str1, str2, 0, 0)

    def helper(self, str1, str2, idx1, idx2):
        if idx1 == len(str1):
            return str2[idx2:]
        if idx2 == len(str2):
            return str1[idx1:]

        if str1[idx1] == str2[idx2]:
            return str1[idx1] + self.helper(str1, str2, idx1 + 1, idx2 + 1)

        res1 = str1[idx1] + self.helper(str1, str2, idx1 + 1, idx2)
        res2 = str2[idx2] + self.helper(str1, str2, idx1, idx2 + 1)
        return res1 if len(res1) < len(res2) else res2
```
Pretty similar to the longesto common subsequence, isn't it?

Now, let's try to cache this solution:
```python
class Solution:
    def shortestCommonSupersequence(self, str1: str, str2: str) -> str:
        cache = {}
        return self.helper(str1, str2, 0, 0, cache)

    def helper(self, str1, str2, idx1, idx2, cache):
        if idx1 == len(str1):
            return str2[idx2:]
        if idx2 == len(str2):
            return str1[idx1:]
        if (idx1, idx2) in cache:
            return cache[(idx1, idx2)]

        if str1[idx1] == str2[idx2]:
            cache[(idx1, idx2)] = str1[idx1] + self.helper(str1, str2, idx1 + 1, idx2 + 1, cache)
        else:
            res1 = str1[idx1] + self.helper(str1, str2, idx1 + 1, idx2, cache)
            res2 = str2[idx2] + self.helper(str1, str2, idx1, idx2 + 1, cache)
            cache[(idx1, idx2)] = res1 if len(res1) < len(res2) else res2
            
        return cache[(idx1, idx2)]
```
This solution is nice but think at the space complexity. We have a table (or a hashmap) with size N * M. And each of its element can contain a string of length N + M. So the space complexity is O((N * M)(N + M)).

In order to optimize this solution, we have to turn it up into the interative bottom-up version:
```python
class Solution:
    def shortestCommonSupersequence(self, str1: str, str2: str) -> str:
        dp = [ [""] * (len(str2) + 1) for _ in range(len(str1) + 1)]

        for idx1 in range(len(str1)):
            dp[idx1][-1] = str1[idx1:]
        for idx2 in range(len(str2)):
            dp[-1][idx2] = str2[idx2:]
        
        for idx1 in range(len(str1) - 1, -1, -1):
            for idx2 in range(len(str2) - 1, -1, -1):
                if str1[idx1] == str2[idx2]:
                    dp[idx1][idx2] = str1[idx1] + dp[idx1 + 1][idx2 + 1]
                elif len(dp[idx1 + 1][idx2]) < len(dp[idx1][idx2 + 1]):
                    dp[idx1][idx2] = str1[idx1] + dp[idx1 + 1][idx2]
                else:
                    dp[idx1][idx2] = str2[idx2] + dp[idx1][idx2 + 1]

        return dp[0][0]
```
Now, note that this solution, at each step, only needs the previous row and not the entire grid. So, we can store just two rows of the `dp` grid to optimize it. In this way, we end up with a solution of space complexity of O(N * (N +  M)).