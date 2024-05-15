## [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

<h2 style="color:#ff375f">Hard</h2>
You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

## Solution
```python
import collections

class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        queue = collections.deque()
        max_sliding_window = []

        for idx in range(len(nums)):
            while len(queue) > 0 and queue[-1] < nums[idx]:
                queue.pop()
            queue.append(nums[idx])
            
            if idx >= k and queue[0] == nums[idx - k]:
                queue.popleft()

            if idx >= k - 1:
                max_sliding_window.append(queue[0])

        return max_sliding_window        
```

## Notes
You should use a deque, which provides insertion/deletion of elements in O(1) time both to the left and right side.
Most specifically, the deque must be a monotonic decreasing deque.

So, loop over the array and perform these 3 steps to success:
- Insert the current element to the right side of the deque. Before inserting it, pop every element which is lower than the current element.
- The first element of the deque is the greatest one. Before inserting it into the result, check that it is still inside the current window of length k. If not, remove it from the deque: note that this time you have to remove the element from the left side (that's why it is crucial to use a deque instead of a simple stack).
- Finnaly, insert the first element of the deque into the result.