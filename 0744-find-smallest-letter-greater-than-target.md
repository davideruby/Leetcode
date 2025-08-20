## [744. Find Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target/)

${\textsf{\color{green}Easy}}$

You are given an array of characters letters that is sorted in non-decreasing order, and a character target. There are at least two different characters in letters.

Return the smallest character in letters that is lexicographically greater than target. If such a character does not exist, return the first character in letters.

## Solution
```python
class Solution:
    def nextGreatestLetter(self, letters: List[str], target: str) -> str:
        for char in letters:
            if ord(char) > ord(target):
                return char

        return letters[0]
```
