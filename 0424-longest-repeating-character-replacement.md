## [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)

<h2 style="color:#fac31d">Medium</h2>

You are given a string s and an integer k. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most k times.

Return the length of the longest substring containing the same letter you can get after performing the above operations.

## Solution
```python
# first version: O(26*n)
class Solution:
    def getNumberReplacements(self, left: int, right: int, chars_count: Dict[str, int]) -> int:
        max_char_count = max(chars_count.values())
        current_win_len = right - left + 1
        replacements = current_win_len - max_char_count
        return replacements

    def characterReplacement(self, s: str, k: int) -> int:
        left = 0
        right = 0
        max_len = 0
        chars_count = { }
        max_count = 0

        while right < len(s):
            right_char = s[right]
            chars_count[right_char] = chars_count.get(right_char, 0) + 1

            replacements = self.getNumberReplacements(left, right, chars_count)

            while replacements > k:
                left_char = s[left]
                chars_count[left_char] -= 1
                left += 1
                replacements = self.getNumberReplacements(left, right, chars_count)

            current_win_len = right - left + 1
            if current_win_len > max_len:
                max_len = current_win_len
            right += 1
        return max_len

# second version: O(n)
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        left = 0
        right = 0
        max_len = 0
        chars_count = { }
        max_count = 0

        for right, right_char in enumerate(s):
            chars_count[right_char] = chars_count.get(right_char, 0) + 1

            if chars_count[right_char] > max_count:
                max_count = chars_count[right_char]

            current_window_len = right - left + 1
            replacements = current_window_len - max_count

            if replacements > k:
                left_char = s[left]
                chars_count[left_char] -= 1
                left += 1
            else:
                current_win_len = right - left + 1
                if current_win_len > max_len:
                    max_len = current_win_len

        return max_len
```

## Notes
- This should be hard in my opinion. There are two solutions, but both have the idea that the number of replacements is: - `replacements = current_window_len - max_count`, where `max_count` is the frequence of the most appearing character in the current window. 
- The first solution is to keep track of the frequencies of each character with a hashmap, and, each time we have to determine `max_count`, we loop over this hash_map which is max of 26 characters. So the complexity of this version of the solution is `O(26*n)` 
- The second solution still uses the hash_map but keeps track of the `max_count` through a variable, which is updated each time the character and right position is processed.
  `max_count` could be unconsistent at some time in the algorithm, but since we want to find the maximum substring length, it's not a real problem.
