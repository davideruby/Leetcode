## [1422. Maximum Score After Splitting a String](https://leetcode.com/problems/maximum-score-after-splitting-a-string/)

${\textsf{\color{green}Easy}}$

Given a string s of zeros and ones, return the maximum score after splitting the string into two non-empty substrings (i.e. left substring and right substring).

The score after splitting a string is the number of zeros in the left substring plus the number of ones in the right substring.

## Solution
```python
class Solution:
    def maxScore(self, s: str) -> int:
        # prefix sum of zeros
        zeros = [0] * len(s)
        for idx in range(len(s)):
            if s[idx] == "0":
                zeros[idx] += 1
            if idx > 0:
                zeros[idx] += zeros[idx - 1]
        
        # prefix sum of ones
        ones = [0] * len(s)
        for idx in range(len(s) - 1, -1, -1):
            if s[idx] == "1":
                ones[idx] += 1
            if idx < len(s) - 1:
                ones[idx] += ones[idx + 1]

        # get the max score
        max_score = 0
        for idx in range(len(s) - 1):
            max_score = max(max_score, zeros[idx] + ones[idx + 1])

        return max_score
```

## Notes
Compute a prefix sum of ones and zeros.
