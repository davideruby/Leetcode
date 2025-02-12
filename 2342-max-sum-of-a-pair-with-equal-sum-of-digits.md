## [2342. Max Sum of a Pair With Equal Sum of Digits](https://leetcode.com/problems/max-sum-of-a-pair-with-equal-sum-of-digits/)

${\textsf{\color{yellow}Medium}}$

You are given a 0-indexed array nums consisting of positive integers. You can choose two indices i and j, such that i != j, and the sum of digits of the number nums[i] is equal to that of nums[j].

Return the maximum value of nums[i] + nums[j] that you can obtain over all possible indices i and j that satisfy the conditions.

## Solution
```python
class Solution:
    def maximumSum(self, nums: List[int]) -> int:
        digits = {}
        max_sum = -1

        for num in nums:
            digit_sum = self.getDigitSum(num)
            
            if digit_sum in digits:
                max_sum = max(max_sum, num + digits[digit_sum])    
            
            digits[digit_sum] = max(digits.get(digit_sum, -1), num)

        return max_sum

    def getDigitSum(self, num):
        digit_sum = 0

        while num > 0:
            digit_sum += num % 10
            num //= 10
        
        return digit_sum
```

## Notes
At first, I built a solution that used a max-heap to store the numbers for each digit sum. This solution is the following and has `O(n logn)` time complexity:

```python
import heapq

class Solution:
    def maximumSum(self, nums: List[int]) -> int:
        digits = {}

        for num in nums:
            digit_sum = self.getDigitSum(num)
            if digit_sum not in digits:
                digits[digit_sum] = []
            
            heapq.heappush(digits[digit_sum], -num)

        max_sum = -1
        for heap in digits.values():
            if len(heap) >= 2:
                num1 = -heapq.heappop(heap)
                num2 = -heapq.heappop(heap)
                max_sum = max(max_sum, num1 + num2)
        
        return max_sum

    def getDigitSum(self, num):
        digit_sum = 0

        while num > 0:
            digit_sum += num % 10
            num //= 10
        
        return digit_sum
```

Then, I realized that no heap is needed, since it is sufficient to store for each digit sum the maximum number in a hashmap. In this way we get a solution with O(n) time complexity.