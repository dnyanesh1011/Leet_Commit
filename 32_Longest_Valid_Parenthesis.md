# Longest Valid Parentheses

## Problem Description

Given a string containing just the characters `'('` and `')'`, return the length of the longest valid (well-formed) parentheses substring.

A valid substring is defined as one where every opening parenthesis `(` has a matching closing parenthesis `)` and vice versa.

---

## Examples

### Example 1:

**Input**:  
```plaintext
s = "(()"
```

**Output**:  
```plaintext
2
```

**Explanation**:  
The longest valid parentheses substring is `"()"`.

---

### Example 2:

**Input**:  
```plaintext
s = ")()())"
```

**Output**:  
```plaintext
4
```

**Explanation**:  
The longest valid parentheses substring is `"()()"`.

---

### Example 3:

**Input**:  
```plaintext
s = ""
```

**Output**:  
```plaintext
0
```

**Explanation**:  
An empty string has no valid substrings.

---

## Approach

### Key Insights

1. **Using a Stack**:  
   - A stack helps to match opening and closing parentheses while keeping track of their positions.

2. **Tracking Invalid Indices**:  
   - Maintain indices of unmatched parentheses to calculate the length of valid substrings.

3. **Two-Pass Scanning (Optional Alternative)**:  
   - Traverse the string twice (left-to-right and right-to-left) to count valid substrings using counters for open and close parentheses.

---

## Solution Steps

1. **Initialize a Stack**:  
   - Store indices of unmatched parentheses.  
   - Push `-1` initially to handle edge cases where the valid substring starts from the beginning.

2. **Iterate Through the String**:  
   - For an opening parenthesis `'('`, push its index onto the stack.
   - For a closing parenthesis `')'`, pop the stack:
     - If the stack becomes empty, push the current index to reset the base for the next valid substring.
     - Otherwise, calculate the length of the current valid substring using the difference between the current index and the top of the stack.

3. **Return the Maximum Length**:  
   - Track the maximum length of valid substrings during the traversal.

---

## Complexity Analysis

### Time Complexity:
- **Single Pass**: \(O(n)\), where \(n\) is the length of the string.  
- The stack operations (push/pop) are \(O(1)\), so the traversal is linear.

### Space Complexity:
- **Stack Usage**: \(O(n)\), where \(n\) is the length of the string in the worst case.

---

## Solution Code

### C++ Implementation

```cpp
class Solution {
public:
    int longestValidParentheses(string s) {
        stack<int> stack;
        stack.push(-1); // Base index for calculating lengths
        int max_length = 0;

        for (int i = 0; i < s.size(); ++i) {
            if (s[i] == '(') {
                stack.push(i); // Push index of '(' onto the stack
            } else {
                stack.pop(); // Pop the top for ')'
                if (stack.empty()) {
                    stack.push(i); // Reset the base index
                } else {
                    max_length = max(max_length, i - stack.top());
                }
            }
        }

        return max_length;
    }
};

```

---

## Example Walkthrough

### Input: `s = ")()())"`

1. **Initial Stack**: `[-1]`  
   **Max Length**: `0`

2. **Iteration**:
   - `i = 0, char = ')'`: Stack becomes empty after popping. Push current index: `stack = [0]`.
   - `i = 1, char = '('`: Push index: `stack = [0, 1]`.
   - `i = 2, char = ')'`: Pop top, calculate length: `2 - stack[-1] = 2`. Update max length: `max_length = 2`.
   - `i = 3, char = '('`: Push index: `stack = [0, 3]`.
   - `i = 4, char = ')'`: Pop top, calculate length: `4 - stack[-1] = 4`. Update max length: `max_length = 4`.
   - `i = 5, char = ')'`: Stack becomes empty after popping. Push current index: `stack = [5]`.

3. **Output**: `max_length = 4`.

---

## Edge Cases

1. **Empty String**:  
   Input: `s = ""`  
   Output: `0`  

2. **No Valid Parentheses**:  
   Input: `s = "(((("` or `s = "))))"`  
   Output: `0`  

3. **All Valid Parentheses**:  
   Input: `s = "()" * 5000`  
   Output: `10000` (handles large inputs efficiently).

---

## Optimizations

- A two-pointer approach with two scans (left-to-right and right-to-left) can achieve the same result without extra space for the stack. However, the stack-based approach is easier to implement and debug.
