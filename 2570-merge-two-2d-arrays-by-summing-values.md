## [2570. Merge Two 2D Arrays by Summing Values](https://leetcode.com/problems/merge-two-2d-arrays-by-summing-values/)

${\textsf{\color{green}Easy}}$

You are given two 2D integer arrays nums1 and nums2.

- nums1[i] = [idi, vali] indicate that the number with the id idi has a value equal to vali.
- nums2[i] = [idi, vali] indicate that the number with the id idi has a value equal to vali.

Each array contains unique ids and is sorted in ascending order by id.

Merge the two arrays into one array that is sorted in ascending order by id, respecting the following conditions:

- Only ids that appear in at least one of the two arrays should be included in the resulting array.
- Each id should be included only once and its value should be the sum of the values of this id in the two arrays. If the id does not exist in one of the two arrays, then assume its value in that array to be 0.

Return the resulting array. The returned array must be sorted in ascending order by id.

## Solution
```python
class Solution:
    def mergeArrays(self, nums1: List[List[int]], nums2: List[List[int]]) -> List[List[int]]:
        merged = []
        idx1 = 0
        idx2 = 0

        while idx1 < len(nums1) and idx2 < len(nums2):
            id1, val1 = nums1[idx1]
            id2, val2 = nums2[idx2]

            if id1 == id2:
                merged.append([id1, val1 + val2])
                idx1 += 1
                idx2 += 1
            elif id1 < id2:
                merged.append([id1, val1])
                idx1 += 1
            else:
                merged.append([id2, val2])
                idx2 += 1

        while idx1 < len(nums1):
            merged.append(nums1[idx1])
            idx1 += 1

        while idx2 < len(nums2):
            merged.append(nums2[idx2])
            idx2 += 1

        return merged
```

## Notes
Use two pointers.
