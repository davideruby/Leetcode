## [567. Permutation in String](https://leetcode.com/problems/permutation-in-string/)

<h2 style="color:#fac31d">Medium</h2>

Given two strings s1 and s2, return true if s2 contains a permutation of s1, or false otherwise.

In other words, return true if one of s1's permutations is the substring of s2.

## Solution
```python
# Time: O(26 + n + m) = O(n + m), Space: O(26) = O(1)
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        needs = { chr(char): 0 for char in range(ord('a'), ord('z') + 1) }
        for char1 in s1:
            needs[char1] += 1

        count_needs = len([1 for count in needs.values() if count > 0])
        have = { chr(char): 0 for char in range(ord('a'), ord('z') + 1) }
        left = 0
        for right_char in s2:
            have[right_char] += 1

            if have[right_char] == needs[right_char]:
                count_needs -= 1

            while have[right_char] > needs[right_char]:
                left_char = s2[left]
                if have[left_char] == needs[left_char]:
                    count_needs += 1
                have[left_char] -= 1
                left += 1

            if count_needs == 0:
                return True

        return False
```

## Notes
- I used a sliding window and two hashmaps. The first hashmaps `have` contains for each characters how many ones I have, the other hashmap `needs` contains for each characters how many I need. When I find that the `have[character] > needs[character]`, I increase the left index and update `have`.
