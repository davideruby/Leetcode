## [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)

<h2 style="color:#fac31d">Medium</h2>
Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

## Solution
```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        counts = {}

        for num in nums:
            counts[num] = counts.get(num, 0) + 1

        count_to_numbers = []
        for idx in range(len(nums) + 1):
            count_to_numbers.append([])

        for num, count in counts.items():
            count_to_numbers[count].append(num)

        result = []
        for count in range(len(count_to_numbers) - 1, -1, -1):
            for num in count_to_numbers[count]:
                result.append(num)
            if len(result) == k:
                break

        return result
```

## Notes
Use a hashmap to count how many times each number appears. Then use an array `count_to_numbers` from 1 to N, such that `count_to_numbers[i]` contains a list of the numbers appearing `i` times.
