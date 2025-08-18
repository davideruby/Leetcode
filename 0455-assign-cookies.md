## [455. Assign Cookies](https://leetcode.com/problems/assign-cookies/)

${\textsf{\color{green}Easy}}$

Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie.

Each child i has a greed factor g[i], which is the minimum size of a cookie that the child will be content with; and each cookie j has a size s[j]. If s[j] >= g[i], we can assign the cookie j to the child i, and the child i will be content. Your goal is to maximize the number of your content children and output the maximum number.

## Solution
```python
class Solution:
    def findContentChildren(self, g: List[int], s: List[int]) -> int:
        g.sort()
        s.sort()
        idx_s = 0
        idx_g = 0

        while idx_s < len(s) and idx_g < len(g):
            greed = g[idx_g]
            feed = s[idx_s]

            if greed <= feed:
                idx_g += 1
                idx_s += 1
            else:
                idx_s += 1
        
        return idx_g
```

## Notes
Sort both `g` and `s` and use a greedy approach. 
Time complexity: `O(mlogm + nlogn)`.