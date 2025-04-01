## [2140. Solving Questions With Brainpower](https://leetcode.com/problems/solving-questions-with-brainpower/)

${\textsf{\color{yellow}Medium}}$

You are given a 0-indexed 2D integer array questions where questions[i] = [pointsi, brainpoweri].

The array describes the questions of an exam, where you have to process the questions in order (i.e., starting from question 0) and make a decision whether to solve or skip each question. Solving question i will earn you pointsi points but you will be unable to solve each of the next brainpoweri questions. If you skip question i, you get to make the decision on the next question.

- For example, given questions = [[3, 2], [4, 3], [4, 4], [2, 5]]:
    - If question 0 is solved, you will earn 3 points but you will be unable to solve questions 1 and 2.
    - If instead, question 0 is skipped and question 1 is solved, you will earn 4 points but you will be unable to solve questions 2 and 3.

Return the maximum points you can earn for the exam.

## Solution
```python
class Solution:
    def mostPoints(self, questions: List[List[int]]) -> int:
        dp = [0] * len(questions)

        for idx in range(len(questions) - 1, -1, -1):
            points, brainpower = questions[idx]
            
            solve = points
            if idx + brainpower + 1 < len(questions):
                solve += dp[idx + brainpower + 1]

            skip = 0
            if idx + 1 < len(questions):
                skip += dp[idx + 1]
            
            dp[idx] = max(solve, skip)

        return dp[0]
```

## Notes
This is a pretty straightforward dynamic programming problem.

The brute-force recursive solutions is the following:
```python
class Solution:
    def mostPoints(self, questions: List[List[int]]) -> int:
        return self.maxPoints(questions, 0)
        
    def maxPoints(self, questions, idx):
        if idx >= len(questions):
            return 0

        points, brainpower = questions[idx]
        solve = points + self.maxPoints(questions, idx + brainpower + 1, cache)
        skip = self.maxPoints(questions, idx + 1, cache)
        return max(solve, skip)
```

Then, it can be cached:
```python
class Solution:
    def mostPoints(self, questions: List[List[int]]) -> int:
        return self.maxPoints(questions, 0, {})

    def maxPoints(self, questions, idx, cache):
        if idx >= len(questions):
            return 0
        if idx in cache:
            return cache[idx]

        points, brainpower = questions[idx]
        solve = points + self.maxPoints(questions, idx + brainpower + 1, cache)
        skip = self.maxPoints(questions, idx + 1, cache)
        cache[idx] = max(solve, skip)
        return cache[idx]
```

And finally we can turn it into the iterative bottom-up version.