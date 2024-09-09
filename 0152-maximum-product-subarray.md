## [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)

<h2 style="color:#fac31d">Medium</h2>

Given an integer array nums, find a subarray that has the largest product, and return the product.

The test cases are generated so that the answer will fit in a 32-bit integer.

## Solution
```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        left = 1
        right = 1
        max_product = nums[0]

        for idx in range(len(nums)):
            if left == 0:
                left = 1
            left *= nums[idx]

            if right == 0:
                right = 1
            right *= nums[-(idx + 1)]

            max_product = max(max_product, left, right)
        
        return max_product
```

## Notes
I found a lot of different approaches to solve this problem and this is the one I prefer the most.
The important point of every approach is that we have to build a solution which deals with these 3 cases:
1. All the elements are positive: then your answer will be the product of all the elements in the array.
2. Array has both positive and negative elements. If the number of negative numbers is even, then again your answer will be complete array. If the number of negative numbers is odd, then you have to remove just one negative element, either from the left or from the right.
3. Array also contains `0`: in this case you should consider the input array as multiple subarrays where the max product will be in one of them.

The approach I used here calculate the max prefix product (`left`) and the max suffix product (`right`) works as follows:
1. If all the elements are positive, then the answer will be in both `left` and `right`.
2. If negative elements are even, same as 1. If negative numbers are odd, then the negative element to remove will be either to the right or to the left. But since we calculate both the max prefix product and the max suffix product, our answer will be the maximum of them.
3. Whenever we encounter a 0, we have to reinitialize `left` or `right` to `1`, in order to restart our search for the max product.
