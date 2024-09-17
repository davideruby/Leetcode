## [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)

<h2 style="color:#00b8a3">Easy</h2>
Given two strings s and t, return true if t is an anagram of s, and false otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Solution
```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        letters = {}

        for i in range(len(s)):
            letters[s[i]] = letters.get(s[i], 0) + 1
            letters[t[i]] = letters.get(t[i], 0) - 1


        for count in letters.values():
            if count != 0:
                return False
        return True
```

## Notes
Use a hashmap to count how many times each character appears. When we found the character in `s` we increase the counter, when in `t` we decrease it. At the end, if all the counters are zero, `s` and `t` are anagrams.
