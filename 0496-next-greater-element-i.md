## [496. Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/)

<h2 style="color:#00b8a3">Easy</h2>

The next greater element of some element x in an array is the first greater element that is to the right of x in the same array.

You are given two distinct 0-indexed integer arrays nums1 and nums2, where nums1 is a subset of nums2.

For each 0 <= i < nums1.length, find the index j such that nums1[i] == nums2[j] and determine the next greater element of nums2[j] in nums2. If there is no next greater element, then the answer for this query is -1.

Return an array ans of length nums1.length such that ans[i] is the next greater element as described above.

## Solution
```python
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        next_gt_el = {}
        stack = []
        for idx, num2 in enumerate(nums2):
            next_gt_el[num2] = -1
            while len(stack) > 0 and num2 > stack[-1]:
                lower_num = stack.pop()
                next_gt_el[lower_num] = num2
            stack.append(num2)

        return [next_gt_el[num1] for num1 in nums1]
```

## Notes
Use a monotonic stack: while the current element is greater than the top of the stack, pop the number from the stack and set the current element as his next greater element (in a hashmap).
