## [978. Longest Turbulent Subarray](https://leetcode.com/problems/longest-turbulent-subarray/)

<h2 style="color:#fac31d">Medium</h2>

Given an integer array arr, return the length of a maximum size turbulent subarray of arr.

A subarray is turbulent if the comparison sign flips between each adjacent pair of elements in the subarray.

More formally, a subarray [arr[i], arr[i + 1], ..., arr[j]] of arr is said to be turbulent if and only if:

For i <= k < j:
- arr[k] > arr[k + 1] when k is odd, and
- arr[k] < arr[k + 1] when k is even.

Or, for i <= k < j:
- arr[k] > arr[k + 1] when k is even, and
- arr[k] < arr[k + 1] when k is odd.

## Solution
```python
class Solution:
    def maxTurbulenceSize(self, arr: List[int]) -> int:
        max_turbulence_size = 1
        is_turbulent = False
        next_check = ""
        turbulence_size = 0

        for idx in range(1, len(arr)):
            if not is_turbulent:
                turbulence_size = 1
                if arr[idx - 1] > arr[idx]:
                    turbulence_size += 1
                    next_check = "<"
                elif arr[idx - 1] < arr[idx]:
                    turbulence_size += 1
                    next_check = ">"

            if idx < len(arr) - 1:
                if next_check == ">":
                    is_turbulent = arr[idx] > arr[idx + 1]
                    next_check = "<"
                else:
                    is_turbulent = arr[idx] < arr[idx + 1]
                    next_check = ">"
            else:
                is_turbulent = False

            if is_turbulent:
                turbulence_size += 1

            if turbulence_size > max_turbulence_size:
                max_turbulence_size = turbulence_size

        return max_turbulence_size
```

## Notes
I found this problem kinda tricky. Solved with a sort of Kadane's algorithm.
