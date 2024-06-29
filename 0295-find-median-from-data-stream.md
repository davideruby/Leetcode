## [295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)

<h2 style="color:#ff375f">Hard</h2>
The median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value, and the median is the mean of the two middle values.

- For example, for arr = [2,3,4], the median is 3.
- For example, for arr = [2,3], the median is (2 + 3) / 2 = 2.5.


Implement the MedianFinder class:

- MedianFinder() initializes the MedianFinder object.
- void addNum(int num) adds the integer num from the data stream to the data structure.
- double findMedian() returns the median of all elements so far. Answers within 10-5 of the actual answer will be accepted.

## Solution
```python
import heapq

class MedianFinder:

    def __init__(self):
        self.left = []
        self.right = []

    def addNum(self, num: int) -> None:
        heapq.heappush(self.left, -num)

        if len(self.right) > 0 and -self.left[0] > self.right[0]:
            heapq.heappush(self.right, -heapq.heappop(self.left))

        if len(self.left) > len(self.right) + 1:
            heapq.heappush(self.right, -heapq.heappop(self.left))
        elif len(self.right) > len(self.left) + 1:
            heapq.heappush(self.left, -heapq.heappop(self.right))

    def findMedian(self) -> float:
        if len(self.left) > len(self.right):
            return -self.left[0]
        elif len(self.right) > len(self.left):
            return self.right[0]
        else:
            return (-self.left[0] + self.right[0]) / 2
```

## Notes
This solution uses two heaps: `left`, a max-heap, and `right`, a min-heap.
The idea is to insert the numbers in these two heaps so that the length of them differs for maximum one, and every element in `left` is smaller than each element of `right`.
For example, let's say we have to insert the sequence `[3, 2, 10, 7, 9]`:
- `left` will contain the first 3 elements: `[7, 3, 2]`,
- `right` will contain the other 2 elements: `[9, 10]`.

In this way, when we have to find the median:
- if `left` is larger then right, we return `left[0]`,
- if `right` is larger then left, we return `right[0]`,
- if `left` and `right` have same length, we return the average between `left[0]` and `right[0]`.
