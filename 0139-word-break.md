## [139. Word Break](https://leetcode.com/problems/word-break/)

<h2 style="color:#fac31d">Medium</h2>

Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.

Note that the same word in the dictionary may be reused multiple times in the segmentation.

## Solution
```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        dp = [False] * (len(s))

        for idx in range(len(s)):
            for jdx in range(idx, -1, -1):
                if s[jdx:idx + 1] in wordDict and (jdx == 0 or dp[jdx - 1]):
                    dp[idx] = True
                    break
        
        return dp[len(s) - 1]
```

## Notes
This is a dynamic programming problem. 

The first solution I came up with was the simple recursion: 
```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        if s in wordDict:
            return True
        
        for idx in range(len(s)):
            if s[:idx] in wordDict and self.wordBreak(s[idx:], wordDict):
                return True
        
        return False
```
For example, if `s = "ABCD"`, then `s` is breakable if:
- `"A" in wordDict` and `"BCD"` is breakable, or
- `"AB" in wordDict` and `"CD"` is breakable, or
- `"ABC" in wordDict` and `"D"` is breakable, or
- `"ABCD" in wordDict`.

Then, I used a `cache` to speed up the solution:
```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        return self.wordBreakCached(s, wordDict, {})


    def wordBreakCached(self, s: str, wordDict: List[str], cache: Dict[str, bool]) -> bool:
        if s in wordDict:
            return True

        if s not in cache:
            cache[s] = False

            for idx in range(1, len(s) + 1):
                if s[:idx] in wordDict and self.wordBreakCached(s[idx:], wordDict, cache):
                    cache[s] = True
                    break

        return cache[s]
```

And, finally, I turned this solution to the iterative version. 
This latter approach uses a `dp` array, where `dp[i] = True` if `s[:i + 1]` is breakable.