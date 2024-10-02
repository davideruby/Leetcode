## [846. Hand of Straights](https://leetcode.com/problems/hand-of-straights/)

<h2 style="color:#fac31d">Medium</h2>
Alice has some number of cards and she wants to rearrange the cards into groups so that each group is of size groupSize, and consists of groupSize consecutive cards.

Given an integer array hand where hand[i] is the value written on the ith card and an integer groupSize, return true if she can rearrange the cards, or false otherwise.

## Solution
```python
from collections import Counter 
import heapq

class Solution:
    def isNStraightHand(self, hand: List[int], groupSize: int) -> bool:
        counts = Counter(hand)
        heapq.heapify(hand)

        while len(hand) > 0:
            group_start = heapq.heappop(hand)
            if counts[group_start] > 0 and not self.canFormGroup(group_start, hand, groupSize, counts):
                return False
        return True


    def canFormGroup(self, start: int, hand: List[int], groupSize: int, counts: Dict[int, int]):
        for required_card in range(start, start + groupSize):
            if counts.get(required_card, 0) == 0:
                return False
            counts[required_card] -= 1
        
        return True
```

## Notes
At first, count how many occurences we have for each card. 
Then, `heapify` the array `hand`, because we have to take the smallest card in `O(1)`.

In the while loop, we take the smallest card to start forming a group, from `card` to `card + groupSize`. So, every required card to form the group will decrement our `counts` hashmap. If the required `card is not counts` or `counts[card] == 0`, it means we can't form the group so we `return False`.

This algorithm has `O(n * logn)` time complexity because we pop from the heap the smallest card, for each card in the array.