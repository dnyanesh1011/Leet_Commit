# ✖️➕➖➗🟰 Basic Calculator

## Problem Statement

Given a string `s` representing a valid mathematical expression, implement a basic calculator to evaluate it. The string may include:

- **Numbers** (integers only).
- **Operators**: `+` and `-`.
- **Parentheses**: `()` for grouping sub-expressions.
- Spaces, which should be ignored.

### Constraints:
1. `s` will always represent a valid expression.
2. No need to handle multiplication or division operators.
3. Do not use built-in functions like `eval()`.

---

## Examples

### Example 1:
**Input**:  
`s = "1 + 1"`  
**Output**:  
`2`

---

### Example 2:
**Input**:  
`s = " 2-1 + 2 "`  
**Output**:  
`3`

---

### Example 3:
**Input**:  
`s = "(1+(4+5+2)-3)+(6+8)"`  
**Output**:  
`23`

---

## Approach and Solution Explanation

The solution uses a **stack** and a **sign-tracking variable** to evaluate the expression. The core idea is to evaluate the expression incrementally while properly handling parentheses.

### Steps:

1. **Initialize Variables**:
   - `currentResult`: Tracks the current result.
   - `sign`: Tracks the current sign (`+1` or `-1`).
   - `stack`: Used to store intermediate results and signs when encountering parentheses.

2. **Iterate Through the Expression**:
   - If a **digit** is encountered:
     - Read the entire number (it can have multiple digits).
     - Add it to `currentResult` based on the current `sign`.
   - If a **`+`** is encountered:
     - Set `sign = 1`.
   - If a **`-`** is encountered:
     - Set `sign = -1`.
   - If an **`(`** is encountered:
     - Push the current `currentResult` and `sign` onto the stack.
     - Reset `currentResult` and `sign` for the expression inside the parentheses.
   - If a **`)`** is encountered:
     - Pop the last `sign` and `result` from the stack and combine it with the current result.

3. **Return `currentResult`**:
   - After processing all characters in the string.

---

## Solution Code

```cpp
class Solution {
public:
    int calculate(string s) {
        stack<int> stk; // To store previous results and signs
        int currentResult = 0; // Current result of the expression
        int sign = 1; // Current sign (+1 or -1)

        for (int i = 0; i < s.length(); ++i) {
            char ch = s[i];

            if (isdigit(ch)) {
                // Read the full number (to handle multi-digit numbers)
                int num = 0;
                while (i < s.length() && isdigit(s[i])) {
                    num = num * 10 + (s[i] - '0');
                    i++;
                }
                i--; // Adjust for extra increment
                currentResult += sign * num; // Add the number to result based on the sign
            } else if (ch == '+') {
                // Set the sign to positive
                sign = 1;
            } else if (ch == '-') {
                // Set the sign to negative
                sign = -1;
            } else if (ch == '(') {
                // Push the current result and sign onto the stack
                stk.push(currentResult);
                stk.push(sign);
                // Reset the result and sign for the new expression
                currentResult = 0;
                sign = 1;
            } else if (ch == ')') {
                // Pop the sign and previous result from the stack
                int prevSign = stk.top();
                stk.pop();
                int prevResult = stk.top();
                stk.pop();
                // Combine the current result with the previous result
                currentResult = prevResult + prevSign * currentResult;
            }
        }

        return currentResult; // Return the final result
    }
};
```

---

## Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the length of the string. Each character is processed once.
- **Space Complexity**: \(O(n)\), for the stack, in the worst case when there are many nested parentheses.

---

## Edge Cases to Consider

1. **Simple Expressions**:
   - `"1+1"`, `"2-1"`, `"3"`.

2. **Expressions with Parentheses**:
   - `"(1+2)"`, `"((3+4)-5)"`.

3. **Expressions with Spaces**:
   - `"   1+ 2 "`, `"  3 -   (  4 +5 )  "`.

4. **Nested Parentheses**:
   - `"((1+2)+(3+(4-5)))"`.

This approach ensures that all these cases are handled efficiently and correctly!
