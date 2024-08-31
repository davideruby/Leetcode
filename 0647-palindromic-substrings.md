## [647. Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/)

<h2 style="color:#fac31d">Medium</h2>

Given a string s, return the number of palindromic substrings in it.

A string is a palindrome when it reads the same backward as forward.

A substring is a contiguous sequence of characters within the string.

## Solution
```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        count = 0

        for idx in range(len(s)):
            count += self.countPalindrome(s, idx, idx)
            count += self.countPalindrome(s, idx, idx + 1)

        return count


    def countPalindrome(self, s: str, left: int, right: int) -> int:
        count = 0
        
        while left >= 0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
            count += 1
        
        return count
```

## Notes
I enumerate all the palindromes expanding the given string at each possible position.