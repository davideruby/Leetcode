## [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

<h2 style="color:#ff375f">Hard</h2>
Given two strings s and t of lengths m and n respectively, return the minimum window 
substring of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".

The testcases will be generated such that the answer is unique.

## Solution
```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        needs = {}
        for t_char in t:
            needs[t_char] = needs.get(t_char, 0) + 1

        min_win_len = len(s) + 1
        min_win_left = 0
        min_win_right = 0
        found_min_win = False
        left = 0
        right = 0
        have = {}
        count_needs = len(needs.keys())

        for right, right_char in enumerate(s):
            right_char = s[right]
            if right_char in needs:
                have[right_char] = have.get(right_char, 0) + 1
                if have[right_char] == needs[right_char]:
                    count_needs -= 1

            while count_needs == 0:
                current_win_len = right - left + 1
                if current_win_len < min_win_len:
                    found_min_win = True
                    min_win_len = current_win_len
                    min_win_left = left
                    min_win_right = right

                left_char = s[left]
                if left_char in needs:
                    if have[left_char] == needs[left_char]:
                        count_needs += 1
                    have[left_char] -= 1
                left +=1

        return s[min_win_left : min_win_right + 1] if found_min_win else ""
```

## Notes
Use a sliding window to create a window of letters in s, which would have all the characters from t. Once all the characters are covered, move the left pointer and ensure that all the characters are still covered to minimize the subarray size.

