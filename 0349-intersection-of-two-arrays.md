## [349. Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays/)

${\textsf{\color{green}Easy}}$

Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must be unique and you may return the result in any order.

## Solution
```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        nums2_set = set(nums2)
        intersection = set()

        for num in nums1:
            if num in nums2_set:
                intersection.add(num)
        
        return list(intersection)
```

## Notes
Use sets to optimize. This solution has O(n + m) time complexity.
