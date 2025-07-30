## [58. Length of Last Word](https://leetcode.com/problems/length-of-last-word/)

${\textsf{\color{green}Easy}}$

Given a string s consisting of words and spaces, return the length of the last word in the string.

A word is a maximal substring consisting of non-space characters only.

## Solution
```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        idx = len(s) - 1

        while s[idx] == " ":
            idx -= 1
        
        length = 0
        while idx >= 0 and s[idx] != " ":
            idx -= 1
            length += 1

        return length
```
