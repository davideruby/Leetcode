## [5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/description/)

<h2 style="color:#fac31d">Medium</h2>

Given a string s, return the longest palindromic substring in s.

## Solution
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        longest_left = 0
        longest_right = 1

        for idx in range(len(s) - 1):
            for start_left, start_right in [ [idx, idx], [idx, idx + 1] ]: # odd, even
                left, right = self.expand(s, start_left, start_right)
                if right - left > longest_right - longest_left:
                    longest_left = left
                    longest_right = right
        
        return s[longest_left: longest_right]

    
    def expand(self, s: str, left: int, right: int) -> Tuple[int, int]:
        while left >= 0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
        
        return left + 1, right
```

## Notes
We enumerate all palindromic substrings: we expand the given string at each possible position and keep track of the length of the longest palindrome we found.
