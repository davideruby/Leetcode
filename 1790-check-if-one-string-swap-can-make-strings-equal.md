## [1790. Check if One String Swap Can Make Strings Equal](https://leetcode.com/problems/check-if-one-string-swap-can-make-strings-equal/)

${\textsf{\color{green}Easy}}$

You are given two strings s1 and s2 of equal length. A string swap is an operation where you choose two indices in a string (not necessarily different) and swap the characters at these indices.

Return true if it is possible to make both strings equal by performing at most one string swap on exactly one of the strings. Otherwise, return false.

## Solution
```python
class Solution:
    def areAlmostEqual(self, s1: str, s2: str) -> bool:
        different = []

        for idx in range(len(s1)):
            if s1[idx] != s2[idx]:
                different.append(idx)
                if len(different) > 2:
                    return False

        if len(different) == 2:
            idx, jdx = different
            return s1[idx] == s2[jdx] and s1[jdx] == s2[idx]

        return len(different) == 0
```
