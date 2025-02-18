## [1718. Construct the Lexicographically Largest Valid Sequence](https://leetcode.com/problems/construct-the-lexicographically-largest-valid-sequence/)

${\textsf{\color{yellow}Medium}}$

Given an integer n, find a sequence with elements in the range [1, n] that satisfies all of the following:

- The integer 1 occurs once in the sequence.
- Each integer between 2 and n occurs twice in the sequence.
- For every integer i between 2 and n, the distance between the two occurrences of i is exactly i.
The distance between two numbers on the sequence, a[i] and a[j], is the absolute difference of their indices, |j - i|.

Return the lexicographically largest sequence. It is guaranteed that under the given constraints, there is always a solution.

A sequence a is lexicographically larger than a sequence b (of the same length) if in the first position where a and b differ, sequence a has a number greater than the corresponding number in b. For example, [0,1,9,0] is lexicographically larger than [0,1,5,6] because the first position they differ is at the third number, and 9 is greater than 5.

## Solution
```python
class Solution:
    def constructDistancedSequence(self, n: int) -> List[int]:
        return self.backtracking(n, 0, [-1] * (n * 2 - 1), set())

    def backtracking(self, n, idx, current, used):
        if len(used) == n:
            return current

        if current[idx] != -1:
            return self.backtracking(n, idx + 1, current, used)

        for num in range(n, 0, -1):
            if num not in used:
                jdx = idx if num == 1 else idx + num
                if jdx < len(current) and current[jdx] == -1:
                    current[idx] = current[jdx] = num
                    used.add(num)

                    solution = self.backtracking(n, idx + 1, current, used)
                    if solution:
                        return solution

                    current[idx] = current[jdx] = -1
                    used.remove(num)

        return None
```

## Notes
I used a backtracking algorithm with a greedy component: it tries to build the sequence always starting from the largest available number and then it returns the first solution found.
