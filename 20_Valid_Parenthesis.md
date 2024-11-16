# 🧩 Valid Parentheses Check in C++

## Problem Statement
Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['`, and `']'`, determine if the input string is valid. 

A string is considered valid if:
1. Open brackets are closed by the same type of brackets.
2. Open brackets are closed in the correct order.
3. Every closing bracket has a corresponding open bracket.

### Examples

**Example 1**:  
Input: `s = "()"`  
Output: `true`

**Example 2**:  
Input: `s = "()[]{}"`  
Output: `true`

**Example 3**:  
Input: `s = "(]"`  
Output: `false`

**Example 4**:  
Input: `s = "([])"`  
Output: `true`

---

## Approach

The solution uses a **stack** to match the brackets efficiently.

### Steps
1. Use a **map** to store matching pairs of brackets:  
   `{')': '(', '}': '{', ']': '['}`.
2. Traverse the string:
   - If the character is a closing bracket:
     - Check if the stack is empty or if the top of the stack does not match the corresponding open bracket.
     - If so, return `false`.
     - Otherwise, pop the top of the stack.
   - If the character is an open bracket, push it onto the stack.
3. After traversing the string, check if the stack is empty:
   - If empty, the string is valid.
   - Otherwise, it is invalid.

---

## Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the length of the string. Each character is processed once.
- **Space Complexity**: \(O(n)\), for the stack in the worst case (all open brackets).

---

## Solution Code

```cpp
class Solution {
public:
    bool isValid(string s) {
        unordered_map<char, char> bracketPairs = {
            {')', '('},
            {'}', '{'},
            {']', '['}
        };
        
        stack<char> stk;

        for (char ch : s) {
            if (bracketPairs.count(ch)) {
                if (stk.empty() || stk.top() != bracketPairs[ch]) {
                    return false;
                }
                stk.pop();
            } else {
                stk.push(ch);
            }
        }
        
        return stk.empty();
    }
};
```

---

## Example Workflow

### Input: `"([])"`
1. Push `(` → Stack: `(`.
2. Push `[` → Stack: `([`.
3. Match `]` with `[` → Pop → Stack: `(`.
4. Match `)` with `(` → Pop → Stack: Empty.
5. Stack is empty → Return `true`.

### Input: `"(]"`
1. Push `(` → Stack: `(`.
2. Match `]` with `[` → Mismatch → Return `false`.

---

## Edge Cases
1. **Empty String**: `""` → Return `true`.
2. **Single Closing Bracket**: `")"` → Return `false`.
3. **All Opening Brackets**: `"((("` → Return `false`.
4. **Mixed Brackets**: `"([)]"` → Return `false`.

---

## Summary
This solution efficiently validates a string of parentheses using a stack to manage the order of opening and closing brackets. It handles edge cases and ensures correctness by checking each bracket against its expected match.
