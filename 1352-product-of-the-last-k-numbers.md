## [1352. Product of the Last K Numbers](https://leetcode.com/problems/product-of-the-last-k-numbers/)

${\textsf{\color{yellow}Medium}}$

Design an algorithm that accepts a stream of integers and retrieves the product of the last k integers of the stream.

Implement the ProductOfNumbers class:

- ProductOfNumbers() Initializes the object with an empty stream.
- void add(int num) Appends the integer num to the stream.
- int getProduct(int k) Returns the product of the last k numbers in the current list. You can assume that always the current list has at least k numbers.

The test cases are generated so that, at any time, the product of any contiguous sequence of numbers will fit into a single 32-bit integer without overflowing.

## Solution
```python
class ProductOfNumbers:

    def __init__(self):
        self.prefix_prods = []
        

    def add(self, num: int) -> None:
        if num == 0:
            self.prefix_prods = []
        elif len(self.prefix_prods) == 0:
            self.prefix_prods = [num]
        else:
            self.prefix_prods.append(num * self.prefix_prods[-1])


    def getProduct(self, k: int) -> int:
        if k > len(self.prefix_prods):
            return 0
        if k == len(self.prefix_prods):
            return self.prefix_prods[-1]
        
        return self.prefix_prods[-1] // self.prefix_prods[-k - 1]
```

## Notes
Keep all prefix products of numbers in an array. When you have to return the product of the last k elements, return the last product divided by the prefix product of the (k - 1) previous element.

When you meet a zero, reset the prefix products array.
