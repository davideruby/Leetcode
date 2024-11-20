## [1046. Last Stone Weight](https://leetcode.com/problems/last-stone-weight/)

${\textsf{\color{green}Easy}}$

You are given an array of integers stones where stones[i] is the weight of the ith stone.

We are playing a game with the stones. On each turn, we choose the heaviest two stones and smash them together. Suppose the heaviest two stones have weights x and y with x <= y. The result of this smash is:

- If x == y, both stones are destroyed, and
- If x != y, the stone of weight x is destroyed, and the stone of weight y has new weight y - x.

At the end of the game, there is at most one stone left.

Return the weight of the last remaining stone. If there are no stones left, return 0.

## Solution
```python
import heapq

class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        heap = [-stone for stone in stones]
        heapq.heapify(heap)

        while len(heap) > 1:
            y = heapq.heappop(heap)
            x = heapq.heappop(heap)

            if x != y:
                new_stone = y - x
                heapq.heappush(heap, new_stone)
        
        return -heap[0] if heap else 0
```

## Notes
If we use a max heap to get the two biggest stones and insert the new one, we will get `O(n * logn)` time complexity.
If we sort the array, we can get the two biggest stones easily, but we will have to insert the new one in ordered way, and so with time complexity `O(n)`, ending up in an overall time complexity of `O(n^2)`.
