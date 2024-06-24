## [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/description/)

<h2 style="color:#fac31d">Medium</h2>

Given an integer array nums and an integer k, return the kth largest element in the array.

Note that it is the kth largest element in the sorted order, not the kth distinct element.

Can you solve it without sorting?

## Solution
```python
import heapq

class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        heap = []

        for num in nums:
            if len(heap) < k:
                heapq.heappush(heap, num)
            elif num > heap[0]:
                heapq.heappop(heap)
                heapq.heappush(heap, num)
        
        return heap[0]
```

## Notes
For this problem, I like two approaches:
- Use a min heap that stores the kth largest elements and at the end return `heap[0]`. This algorithm has time complexity `O(n*logk)`.
- Use the quickselect algorithm. It has average time complexity of `O(n)`, but in the worst case its time complexity is `O(n^2)` (that's why on Leetcode it ends up in TLE).
