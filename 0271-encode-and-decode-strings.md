## [271. Encode and Decode Strings](https://leetcode.com/problems/encode-and-decode-strings)

<h2 style="color:#fac31d">Medium</h2>

Design an algorithm to encode a list of strings to a single string. The encoded string is then decoded back to the original list of strings.

Please implement encode and decode

## Solution
```python
class Solution:
    
    def encode(self, strs: List[str]) -> str:
        encoded = ""
        for string in strs:
            encoded += str(len(string)) + "!" + string
        return encoded

    def decode(self, s: str) -> List[str]:
        idx = 0
        decoded_strings = []

        while idx < len(s):
            jdx = idx
            while s[jdx] != "!":
                jdx += 1

            start_string = jdx + 1
            num_characters = int(s[idx: jdx])
            end_string = start_string + num_characters
            decoded = s[start_string: end_string]
            decoded_strings.append(decoded)

            idx = end_string
        
        return decoded_strings
```

## Notes
We have to put some separator between one string and another.
Let's consider the character `"!"` as separator.
Just putting `"!"` as separator isn't enough, because `"!"` could be contained in the strings.

So, for each string, we put as separator `N!`, where `N` is the length of the string.
For example, the input `["leet","code","love","you"]` is encoded in `"4!leet4!code4!love3!you"`.

And what if a string contains the separator N!? Just simulate the code, and you'll discover that this algorithm works anyway.
