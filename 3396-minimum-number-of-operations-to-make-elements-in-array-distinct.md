## [3396. Minimum Number of Operations to Make Elements in Array Distinct](https://leetcode.com/problems/minimum-number-of-operations-to-make-elements-in-array-distinct/)

${\textsf{\color{green}Easy}}$

You are given an integer array nums. You need to ensure that the elements in the array are distinct. To achieve this, you can perform the following operation any number of times:

- Remove 3 elements from the beginning of the array. If the array has fewer than 3 elements, remove all remaining elements.

Note that an empty array is considered to have distinct elements. Return the minimum number of operations needed to make the elements in the array distinct.

## Solution
```python
class Solution:
    def minimumOperations(self, nums: List[int]) -> int:
        counter = Counter(nums)
        to_remove = sum([cnt >= 2 for cnt in counter.values()])

        num_ops = 0
        idx = 0
        while to_remove > 0:
            for _ in range(3):
                if idx < len(nums):
                    counter[nums[idx]] -= 1
                    if counter[nums[idx]] == 1:
                        to_remove -= 1
                    idx += 1
            num_ops += 1
        
        return num_ops
```
