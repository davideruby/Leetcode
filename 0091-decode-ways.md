## [91. Decode Ways](https://leetcode.com/problems/decode-ways/)

<h2 style="color:#fac31d">Medium</h2>

You have intercepted a secret message encoded as a string of numbers. The message is decoded via the following mapping:

- "1" -> 'A'
- "2" -> 'B'
- ...
- "25" -> 'Y'
- "26" -> 'Z'

However, while decoding the message, you realize that there are many different ways you can decode the message because some codes are contained in other codes ("2" and "5" vs "25").

For example, "11106" can be decoded into:

- "AAJF" with the grouping (1, 1, 10, 6)
- "KJF" with the grouping (11, 10, 6)
- The grouping (1, 11, 06) is invalid because "06" is not a valid code (only "6" is valid).

Note: there may be strings that are impossible to decode.

Given a string s containing only digits, return the number of ways to decode it. If the entire string cannot be decoded in any valid way, return 0.

The test cases are generated so that the answer fits in a 32-bit integer.

## Solution
```python
class Solution:
    def numDecodings(self, s: str) -> int:
        dec1 = 1
        dec2 = 0

        for idx in range(len(s) - 1, -1, -1):
            tmp = 0
            if s[idx] == "0":
                tmp = 0
            else:
                tmp = dec1
                if idx < len(s) - 1 and (10 <= int(s[idx: idx + 2]) <= 26):
                    tmp += dec2
            
            dec2 = dec1
            dec1 = tmp

        return dec1
```

## Notes
This is a dynamic programming problem. You have to follow step-by-step the path from recursion to dynamic programming:

```python
# 1. Recursion: O(2^n) time, O(1) space
class Solution:
    def numDecodings(self, s: str) -> int:
        if len(s) == 0:
            return 1
        if s[0] == "0":
            return 0
        
        num_decodings = self.numDecodings(s[1:])
        
        if len(s) >= 2 and (10 <= int(s[:2]) <= 26):
            num_decodings += self.numDecodings(s[2:])

        return num_decodings
```

```python
# 2. Memoization: O(n) time, O(n) space
# Introduce a cache to reduce recalculation
class Solution:
    def numDecodings(self, s: str) -> int:
        return self.numDecodingsHelper(s, {})

    def numDecodingsHelper(self, s: str, cache: Dict[str, int]) -> int:
        if len(s) == 0:
            return 1
        if s[0] == "0":
            return 0

        if s not in cache:
            num_decodings = self.numDecodingsHelper(s[1:], cache)
            
            if len(s) >= 2 and (10 <= int(s[:2]) <= 26):
                num_decodings += self.numDecodingsHelper(s[2:], cache)

            cache[s] = num_decodings
        
        return cache[s]
```

```python
# 3. Memoization: O(n) time, O(n) space
# Copy from #2 and avoid recursion calls. 
class Solution:
    def numDecodings(self, s: str) -> int:
        cache = [0] * (len(s) + 1)
        cache[len(s)] = 1

        for idx in range(len(s) - 1, -1, -1):
            cache[idx] = 0
            
            if s[idx] != "0":
                cache[idx] = cache[idx + 1]
                if idx < len(s) - 1 and (10 <= int(s[idx: idx + 2]) <= 26):
                    cache[idx] += cache[idx + 2]
        
        return cache[0]
```

```python
# 4. Memoization with constant space: O(n) time, O(1) space.
# We just need the next 2 elements of the cache, so replace the cache array with two variables.
class Solution:
    def numDecodings(self, s: str) -> int:
        dec1 = 1
        dec2 = 0

        for idx in range(len(s) - 1, -1, -1):
            tmp = 0
            if s[idx] != "0":
                tmp = dec1
                if idx < len(s) - 1 and (10 <= int(s[idx: idx + 2]) <= 26):
                    tmp += dec2
                
            dec2 = dec1
            dec1 = tmp
        
        return dec1
```