## [3136. Valid Word](https://leetcode.com/problems/valid-word/)

${\textsf{\color{green}Easy}}$

A word is considered valid if:

- It contains a minimum of 3 characters.
- It contains only digits (0-9), and English letters (uppercase and lowercase).
- It includes at least one vowel.
- It includes at least one consonant.

You are given a string word.

Return true if word is valid, otherwise, return false.

Notes:

'a', 'e', 'i', 'o', 'u', and their uppercases are vowels.
A consonant is an English letter that is not a vowel.

## Solution
```python
class Solution:
    def isValid(self, word: str) -> bool:
        vowels = set(['A', 'a', 'E', 'e', 'I', 'i', 'O', 'o', 'U', 'u'])
        consonant = False
        vowel = False

        for char in word:
            if char.isupper() or char.islower():
                if char in vowels:
                    vowel = True
                else:
                    consonant = True
            elif not char.isdigit():
                return False
        
        return len(word) >= 3 and vowel and consonant
```
