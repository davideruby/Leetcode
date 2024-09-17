## [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation)

<h2 style="color:#fac31d">Medium</h2>

You are given an array of strings tokens that represents an arithmetic expression in a Reverse Polish Notation.

Evaluate the expression. Return an integer that represents the value of the expression.

Note that:

- The valid operators are '+', '-', '*', and '/'.
- Each operand may be an integer or another expression.
- The division between two integers always truncates toward zero.
- There will not be any division by zero.
- The input represents a valid arithmetic expression in a reverse polish notation.
- The answer and all the intermediate calculations can be represented in a 32-bit integer.

## Solution
```python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        stack = []
        operation_tokens = set(["+", "-", "*", "/"])

        for token in tokens:
            is_operation_token = token in operation_tokens

            if is_operation_token:
                num2 = stack.pop()
                num1 = stack.pop()
                if token == "+":
                    stack.append(num1 + num2)
                elif token == "-":
                    stack.append(num1 - num2)
                elif token == "*":
                    stack.append(num1 * num2)
                else:
                    stack.append(int(num1 / num2))
            else:
                stack.append(int(token))

        return stack.pop()
```

## Notes
Use a stack to store numbers. When you find an operation token, pop the first two elements, perform the operation and push the result onto the stack.
