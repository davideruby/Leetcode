## [97. Interleaving String](https://leetcode.com/problems/interleaving-string/)

${\textsf{\color{yellow}Medium}}$

Given strings s1, s2, and s3, find whether s3 is formed by an interleaving of s1 and s2.

An interleaving of two strings s and t is a configuration where s and t are divided into n and m substrings respectively, such that:

- s = s1 + s2 + ... + sn
- t = t1 + t2 + ... + tm
- |n - m| <= 1
- The interleaving is s1 + t1 + s2 + t2 + s3 + t3 + ... or t1 + s1 + t2 + s2 + t3 + s3 + ...

Note: a + b is the concatenation of strings a and b.

Follow up: Could you solve it using only O(s2.length) additional memory space?

## Solution
```python
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        if len(s1) + len(s2) != len(s3):
            return False

        prev_row = [False] * (len(s2) + 1)
        prev_row[-1] = True
        idx3 = len(s3) - 1
        for idx2 in range(len(s2) - 1, -1, -1):
            prev_row[idx2] = s2[idx2] == s3[idx3] and prev_row[idx2 + 1]
            idx3 -= 1

        idx3 = len(s3) - 1
        for idx1 in range(len(s1) - 1, -1, -1):
            cur_row = [False] * (len(s2) + 1)
            cur_row[-1] = s1[idx1] == s3[idx3] 
            idx3 -= 1
            
            for idx2 in range(len(s2) - 1, -1, -1):
                cur_row[idx2] = (
                    (s1[idx1] == s3[idx1 + idx2] and prev_row[idx2]) or
                    (s2[idx2] == s3[idx1 + idx2] and cur_row[idx2 + 1])
                )
            
            prev_row = cur_row
        
        return prev_row[0]
```

## Notes
This is a dynamic programming problem and this is a super optimized solution. Honestly, I just came up with the top-down recursive solution and I think this solution is not straightforward to understand. Let's go step by step.

The brute-force recursive solution is the one following:
```python
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        if len(s1) + len(s2) != len(s3):
            return False

        def dfs(idx1, idx2):
            if idx1 == len(s1) and idx2 == len(s2):
                return True

            is_interleave = (
                (idx1 < len(s1) and s1[idx1] == s3[idx1 + idx2] and dfs(idx1 + 1, idx2)) or
                (idx2 < len(s2) and s2[idx2] == s3[idx1 + idx2] and dfs(idx1, idx2 + 1)) 
            )

            return is_interleave
        
        return dfs(0, 0)
```
Each time, we check if the current character of either `s1` or `s2` is equal to the current character of `s3` and we update the index of the matching string.

Then, we can memoize this solution:
```python
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        if len(s1) + len(s2) != len(s3):
            return False

        def dfs(idx1: int, idx2: int):
            if idx1 == len(s1) and idx2 == len(s2):
                return True
            if cache[idx1][idx2] is not None:
                return cache[idx1][idx2]

            is_interleave = (
                (idx1 < len(s1) and s1[idx1] == s3[idx1 + idx2] and dfs(idx1 + 1, idx2)) or
                (idx2 < len(s2) and s2[idx2] == s3[idx1 + idx2] and dfs(idx1, idx2 + 1)) 
            )
            
            cache[idx1][idx2] = is_interleave
            return is_interleave
        
        cache = [ [None] * (len(s2) + 1) for _ in range(len(s1) + 1)]
        return dfs(0, 0)
```

Now, to build the super optimized solution, we have to get the bottom-up iterative version of the previous solution:
```python
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        if len(s1) + len(s2) != len(s3):
            return False

        cache = [ [False] * (len(s2) + 1) for _ in range(len(s1) + 1)]
        cache[-1][-1] = True
        idx3 = len(s3) - 1
        for idx1 in range(len(s1) - 1, -1, -1):
            cache[idx1][-1] = s1[idx1] == s3[idx3] and cache[idx1 + 1][-1]
            idx3 -= 1

        idx3 = len(s3) - 1
        for idx2 in range(len(s2) - 1, -1, -1):
            cache[-1][idx2] = s2[idx2] == s3[idx3] and cache[-1][idx2 + 1]
            idx3 -= 1
        
        for idx1 in range(len(s1) - 1, -1, -1):
            for idx2 in range(len(s2) - 1, -1, -1):
                cache[idx1][idx2] = (
                    (s1[idx1] == s3[idx1 + idx2] and cache[idx1 + 1][idx2]) or
                    (s2[idx2] == s3[idx1 + idx2] and cache[idx1][idx2 + 1])
                )

        return cache[0][0]
```
I think the most difficult part of this algorithm is the initialization of the last extra row/colum of the `cache`: they represent the case where `s1` or `s2` is an empty string.

Then, from this solution, you can notice that each time, in order to calculate `cache[idx1][idx2]`, we only need the previous row. So, we can get rid of the matrix and keep track just of the previous row. In this way, we get a solution with `O(s2.length)` space complexity.
