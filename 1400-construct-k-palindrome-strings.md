## [1400. Construct K Palindrome Strings](https://leetcode.com/problems/construct-k-palindrome-strings/)

${\textsf{\color{yellow}Medium}}$

Given a string s and an integer k, return true if you can use all the characters in s to construct k palindrome strings or false otherwise.

## Solution
```python
class Solution:
    def canConstruct(self, s: str, k: int) -> bool:
        hashmap = {}
        for char in s:
            hashmap[char] = hashmap.get(char, 0) + 1

        odd_count = 0
        for count in hashmap.values():
            odd_count += count % 2
        
        return len(s) >= k and odd_count <= k
```

## Notes
If the length of `s` is less than `k`, we obviously return `false`.

When we deal with a character which occures an even number of times, we have no problem.
Let's say we have `s` composed of 2 a's and 2 b's: `aabb`.
We can build up to 1, 2, 3 and 4 palindrome strings, so up to `k = 4` we are ok:
- k = 1: `aabb`
- k = 2: `aba, b`
- k = 3: `b, b, aa`
- k = 4: `a, a, b, b`

Now, let's think about characters having even count. For example, if we have 1 extra c (`s = aabbc`), can we build one palindrome string? Yes, we can: `aacbb`.
And what if we had 3 c's? Can we still build a palindrome string? Of course: `aacccbb`.

But what if we had two character with even count, for example 1 c and 1 d? In this case we can't build a palidrome string (`aacdbb` isn't palindrome).

So, the key of this problem is to count the characters that occure even times in `s` and check the count is less than or equal to `k`.
