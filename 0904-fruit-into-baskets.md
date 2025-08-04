## [904. Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/)

${\textsf{\color{yellow}Medium}}$

You are visiting a farm that has a single row of fruit trees arranged from left to right. The trees are represented by an integer array fruits where fruits[i] is the type of fruit the ith tree produces.

You want to collect as much fruit as possible. However, the owner has some strict rules that you must follow:

- You only have two baskets, and each basket can only hold a single type of fruit. There is no limit on the amount of fruit each basket can hold.
- Starting from any tree of your choice, you must pick exactly one fruit from every tree (including the start tree) while moving to the right. The picked fruits must fit in one of your baskets.
- Once you reach a tree with fruit that cannot fit in your baskets, you must stop.

Given the integer array fruits, return the maximum number of fruits you can pick.

## Solution
```python
class Solution:
    def totalFruit(self, fruits: List[int]) -> int:
        NUM_BASKETS = 2
        count_types = { fruit: 0 for fruit in fruits }
        counts = 0
        max_fruits = 0
        left = 0

        for right, fruit in enumerate(fruits):
            if count_types[fruit] == 0:
                counts += 1
            count_types[fruit] += 1
            
            if counts > NUM_BASKETS:
                count_types[fruits[left]] -= 1
                if count_types[fruits[left]] == 0:
                    counts -= 1
                left += 1

            max_fruits = max(max_fruits, right - left + 1)

        return max_fruits
```

## Notes
This solution uses the same approach described in [76. Minimum Window Substring](./0076-minimum-window-substring.md).
