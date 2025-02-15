## [2698. Find the Punishment Number of an Integer](https://leetcode.com/problems/find-the-punishment-number-of-an-integer/)

${\textsf{\color{yellow}Medium}}$

Given a positive integer n, return the punishment number of n.

The punishment number of n is defined as the sum of the squares of all integers i such that:

- 1 <= i <= n
- The decimal representation of i * i can be partitioned into contiguous substrings such that the sum of the integer values of these substrings equals i.

## Solution
```python
class Solution:
    def punishmentNumber(self, n: int) -> int:
        return sum([num * num for num in range(1, n + 1) if self.canPartition(num)])

    def canPartition(self, num):
        return self.canPartitionHelper(num, str(num * num), 0)
    
    def canPartitionHelper(self, target, str_num, current_sum):
        if str_num == "":
            return current_sum == target

        for idx in range(1, len(str_num) + 1):
            left = str_num[:idx]
            right = str_num[idx:]
            if self.canPartitionHelper(target, right, current_sum + int(left)):
                return True

        return False
```

## Notes
To determine if a number can be partitioned, use a backtracking algorithm.
For example, if you have the number 1234, you should:
- get the sum of 1 + partition(234),
- get the sum of 12 + partition(34),
- get the sum of 123 + partition(4),
- get the sum of 1234.
