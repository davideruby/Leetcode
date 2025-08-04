## [345. Reverse Vowels of a String](https://leetcode.com/problems/reverse-vowels-of-a-string/)

${\textsf{\color{green}Easy}}$

Given a string s, reverse only all the vowels in the string and return it.

The vowels are 'a', 'e', 'i', 'o', and 'u', and they can appear in both lower and upper cases, more than once.

## Solution
```python
class Solution:
    def reverseVowels(self, s: str) -> str:
        vowels = []
        string = list(s)

        for idx, char in enumerate(s):
            if (char == 'a' or char == 'e' or char == 'i' or char == 'o' or char == 'u' or
                char == 'A' or char == 'E' or char == 'I' or char == 'O' or char == 'U'):
                vowels.append(idx)

        left = 0
        right = len(vowels) - 1
        while left < right:
            string[vowels[left]], string[vowels[right]] = string[vowels[right]], string[vowels[left]]
            left += 1
            right -= 1

        return ''.join(string)
```
