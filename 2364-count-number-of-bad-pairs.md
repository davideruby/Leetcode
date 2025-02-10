## [2364. Count Number of Bad Pairs](https://leetcode.com/problems/count-number-of-bad-pairs/)

${\textsf{\color{yellow}Medium}}$

You are given a 0-indexed integer array nums. A pair of indices (i, j) is a bad pair if i < j and j - i != nums[j] - nums[i].

Return the total number of bad pairs in nums.

## Solution
```python
class Solution:
    def countBadPairs(self, nums: List[int]) -> int:
        counter = {}
        for idx, num in enumerate(nums):
            counter[num - idx] = counter.get(num - idx, 0) + 1

        good_pairs = 0
        for count in counter.values():
            good_pairs += (count * (count - 1)) // 2

        total_pairs = (len(nums) * (len(nums) - 1)) // 2
        return total_pairs - good_pairs
```

## Notes
It is better to find the number of bad pairs counting the total pairs and then subtracting the good ones. But how can we count good pairs in O(n) time?

Notice that `j - i == nums[j] - nums[i]` is the same as `j - nums[j] == i - nums[i]`. We can calculate these differences in `O(n)` time and keep a counter of `nums[i] - i` with a hashmap.

Yet, if we find, for example, 4 different elements with the same difference `nums[i] - i`, it means that all the combinations of length 2 of these 4 different elements are good pairs.
And what is the total number of pairs that there are in an array of length n? The number of combinations of length 2 with n elements: `C(n, 2)`. 
So, the first solution I came up with is the following:
```python
from math import comb

class Solution:
    def countBadPairs(self, nums: List[int]) -> int:
        counter = {}
        for idx, num in enumerate(nums):
            counter[num - idx] = counter.get(num - idx, 0) + 1

        good_pairs = 0
        for count in counter.values():
            good_pairs += comb(count, 2)

        total_pairs = comb(len(nums), 2)
        return total_pairs - good_pairs
```

Now, in order to avoid to use the utlity function `comb`, we notice that the number of different combinations of length 2 of n elements is `C(n, 2)` = 
```
   n!                      n * (n - 1) * (n - 2)!             n * (n - 1)
-----------     ----->     ----------------------   ----->  ------------- 
(n - 2)! 2!                     (n - 2)! 2!                       2
```