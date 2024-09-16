## [560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)

<h2 style="color:#fac31d">Medium</h2>

Given an array of integers nums and an integer k, return the total number of subarrays whose sum equals to k.

A subarray is a contiguous non-empty sequence of elements within an array.

## Solution
```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        current_sum = 0
        prefix_sums = {0: 1}
        res = 0

        for num in nums:
            current_sum += num

            if current_sum - k in prefix_sums:
                res += prefix_sums[current_sum - k]

            prefix_sums[current_sum] = prefix_sums.get(current_sum, 0) + 1

        return res
```

## Notes
To explain this problem, I remind you that in python the subarray `nums[:i]` does not include the element `nums[i]`, but only the elements before `i`.

The idea is that we memorize in a hashmap how many sums of `nums[:i]` we have, for each `0 < i <= len(nums)`.

So, let's suppose we are at the element `nums[j]`, then `sum(nums[:j + 1]) = sum(nums[:i]) + sum(nums[i: j + 1])`, for some `i`.
Let's also suppose that the sum of the subarray `nums[i: j + 1]` is equal to our `k`, i.e. `sum(nums[i: j + 1]) = k`.
Then, `sum(nums[:j + 1]) = sum(nums[:i]) + k` ---> `sum(nums[:j + 1]) - k = sum(nums[:i])`. We can check if we have such `sum(nums[:j + 1]) - k` with our hashtable in time `O(1)`.

For example, if we have `nums = [1, 5, 1, 3]` and `k = 6`, when `j = 2` we will have:
`prefix_sums = {0: 1, 1: 1, 6: 1}` and `current_sum = 7`. So, we have to find a previous subarray `nums[:i]` to remove whose sum is `current_sum - k = 1`.
