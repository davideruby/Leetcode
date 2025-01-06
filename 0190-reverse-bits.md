## [190. Reverse Bits](https://leetcode.com/problems/reverse-bits/)

${\textsf{\color{green}Easy}}$

Reverse bits of a given 32 bits unsigned integer.

Note:

- Note that in some languages, such as Java, there is no unsigned integer type. In this case, both input and output will be given as a signed integer type. They should not affect your implementation, as the integer's internal binary representation is the same, whether it is signed or unsigned.
- In Java, the compiler represents the signed integers using 2's complement notation. Therefore, in Example 2 above, the input represents the signed integer -3 and the output represents the signed integer -1073741825.

## Solution
```python
class Solution:
    def reverseBits(self, n: int) -> int:
        reverse = 0

        # for _ in range(32):
        #     reverse = reverse << 1
        #     reverse += n & 1
        #     n = n >> 1

        # or, without bit manipulations:
        for exponent in range(31, -1, -1):
            digit = n % 2
            reverse += digit * (2**exponent)
            n = n // 2

        return reverse
```

## Notes
With the `<<` or `>>` we can shift the bits of a number. So, every time, we shift the bit of `reverse` of 1 position, then we take the last bit of `n` (with `n & 1`) and put it as the last bit of `reverse`:

- n = 10110, last bit is 0, reverse = 0.
- n = 1011, last bit is 1, reverse = 1.
- n = 101, last bit is 1, reverse = 11.
- n = 10, last bit is 0, reverse = 110.
- n = 1, last bit is 1, reverse = 1101.
- n = 0, last bit is 0, reverse = 1101.
