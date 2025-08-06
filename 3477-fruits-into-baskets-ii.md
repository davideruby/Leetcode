## [3477. Fruits Into Baskets II](https://leetcode.com/problems/fruits-into-baskets-ii/)

${\textsf{\color{green}Easy}}$

You are given two arrays of integers, fruits and baskets, each of length n, where fruits[i] represents the quantity of the ith type of fruit, and baskets[j] represents the capacity of the jth basket.

From left to right, place the fruits according to these rules:

- Each fruit type must be placed in the leftmost available basket with a capacity greater than or equal to the quantity of that fruit type.
- Each basket can hold only one type of fruit.
- If a fruit type cannot be placed in any basket, it remains unplaced.

Return the number of fruit types that remain unplaced after all possible allocations are made.

## Solution
```python
class Solution:
    def numOfUnplacedFruits(self, fruits: List[int], baskets: List[int]) -> int:
        available = [True] * len(baskets)

        def getAvailableBasket(fruit):
            for idx, basket in enumerate(baskets):
                if fruit <= basket and available[idx]:
                    return idx
            
            return None

        unplaced = 0
        for fruit in fruits:
            available_basket = getAvailableBasket(fruit)

            if available_basket == None:
                unplaced += 1
            else:
                available[available_basket] = False

        return unplaced
```

## Notes
Can we optimize this, or am I overthinking the optimization?
