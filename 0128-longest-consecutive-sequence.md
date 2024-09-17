## [128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)

<h2 style="color:#fac31d">Medium</h2>

Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.
You must write an algorithm that runs in O(n) time.

## Solution
```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        nums_set = set(nums)

        # It is important to use the set and not the list of nums to perform on a
        # use case containing a lot of repeated numbers.
        longest_seq_len = 0
        for num in nums_set:
            has_previous = (num - 1) in nums_set
            if not has_previous:
                seq_len = 1
                next_num = num + 1
                has_next_num = next_num in nums_set
                while has_next_num:
                    seq_len += 1
                    next_num += 1
                    has_next_num = next_num in nums_set

                if seq_len > longest_seq_len:
                    longest_seq_len = seq_len

        return longest_seq_len
```

## Notes
Store the list in a set. Then loop over the set and check if there is the previous number. If it has not, it means we have a sequence starting from that number. Go ahead until you find the end of the sequence.
