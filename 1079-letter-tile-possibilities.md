## [1079. Letter Tile Possibilities](https://leetcode.com/problems/letter-tile-possibilities/)

${\textsf{\color{yellow}Medium}}$

You have n  tiles, where each tile has one letter tiles[i] printed on it.

Return the number of possible non-empty sequences of letters you can make using the letters printed on those tiles.

## Solution
```python
class Solution:
    def numTilePossibilities(self, tiles: str) -> int:
        return self.helper(Counter(tiles)) - 1

    def helper(self, counts):
        res = 1
        
        for letter in counts:
            if counts[letter] > 0:
                counts[letter] -= 1
                res += self.helper(counts)
                counts[letter] += 1
        
        return res
```

## Notes
Try to build the string with a backtracking DFS by considering what you can put in every position.
