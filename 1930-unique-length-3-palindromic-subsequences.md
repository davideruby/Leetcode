## [1930. Unique Length-3 Palindromic Subsequences](https://leetcode.com/problems/unique-length-3-palindromic-subsequences/)

${\textsf{\color{yellow}Medium}}$

Given a string s, return the number of unique palindromes of length three that are a subsequence of s.

Note that even if there are multiple ways to obtain the same subsequence, it is still only counted once.

A palindrome is a string that reads the same forwards and backwards.

A subsequence of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

For example, "ace" is a subsequence of "abcde".

## Solution
```python
class Solution:
    def countPalindromicSubsequence(self, s: str) -> int:
        first = {}
        last = {}

        for idx, char in enumerate(s):
            if char not in first:
                first[char] = idx
            last[char] = idx

        counts = 0
        for ord_char in range(ord('a'), ord('z') + 1):
            char = chr(ord_char)
            if char in first:
                counts += len(set(s[first[char] + 1: last[char]]))

        return counts
```

## Notes
Kinda tricky problem in my opinion.

The idea is that for each character we keep track of its `first` and last `index` where it appears in the string.
Then, for each character, we count the number of unique characters between `first` and `last`.

The trick is that we can iterate over every letter between 'a' and 'z', because `O(26n) = O(n)`
