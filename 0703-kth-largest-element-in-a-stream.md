## [703. Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/)

<h2 style="color:#00b8a3">Easy</h2>
Design a class to find the kth largest element in a stream. Note that it is the kth largest element in the sorted order, not the kth distinct element.

Implement KthLargest class:

- KthLargest(int k, int[] nums) Initializes the object with the integer k and the stream of integers nums.
- int add(int val) Appends the integer val to the stream and returns the element representing the kth largest element in the stream.

## Solution
```python
import heapq

class KthLargest:

    def __init__(self, k: int, nums: List[int]):
        self.k = k
        self.stream = []
        for num in nums:
            self.add(num)

    def add(self, val: int) -> int:
        if len(self.stream) < self.k:
            heapq.heappush(self.stream, val)
        elif val > self.stream[0]:
            heapq.heappop(self.stream)
            heapq.heappush(self.stream, val)

        return self.stream[0]
```

## Notes
We keep in our class a min heap containing the kth largest element of our stream. 
When we have to insert a value, if it is greater than the head of heap, we pop from the heap and we insert such value.
