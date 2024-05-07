## [1343. Number of Sub-arrays of Size K and Average Greater than or Equal to Threshold](https://leetcode.com/problems/number-of-sub-arrays-of-size-k-and-average-greater-than-or-equal-to-threshold/)

<h2 style="color:#fac31d">Medium</h2>
Given an array of integers arr and two integers k and threshold, return the number of sub-arrays of size k and average greater than or equal to threshold.

## Solution
```python
class Solution:
    def numOfSubarrays(self, arr: List[int], k: int, threshold: int) -> int:
        window_sum = 0
        num_subarrays = 0

        for idx in range(len(arr)):
            window_sum += arr[idx]

            if idx >= k - 1:
                avg = window_sum / k
                if avg >= threshold:
                    num_subarrays += 1
                window_sum -= arr[idx - k + 1]

        return num_subarrays
```

## Notes
Just sum the elements until the sum has size `k`, then check if the average is `>= threshold` and finally remove the first element of the sum, pointed at `idx - k + 1`.
