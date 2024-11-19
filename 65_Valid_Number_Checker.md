# 📖 Valid Number Checker

## Problem Statement

Given a string `s`, determine whether it represents a **valid number**. A valid number can be an integer, a decimal, or a number in scientific notation. Here's the formal definition:

1. **Integer**:
   - An optional `'+'` or `'-'` sign.
   - Followed by one or more digits.
   
2. **Decimal**:
   - An optional `'+'` or `'-'` sign.
   - Either:
     - Digits followed by a dot `'.'`.
     - A dot `'.'` followed by digits.
     - Digits followed by a dot `'.'` and more digits.
   
3. **Scientific Notation**:
   - A number (integer or decimal).
   - Followed by `'e'` or `'E'`.
   - Followed by an integer (an optional `'+'` or `'-'` sign, and digits).

The string may contain leading or trailing spaces, which should be ignored.

### Examples

- **Valid Numbers**:
  - `"2"`, `"0089"`, `"-0.1"`, `"+3.14"`, `"4."`, `"-90E3"`, `"2e10"`, `"53.5e93"`
  
- **Invalid Numbers**:
  - `"abc"`, `"1a"`, `"e3"`, `"99e2.5"`, `"--6"`, `"-+3"`

---

## Approach and Solution Explanation

The solution uses a **step-by-step validation** approach to check the string. Here's the breakdown:

1. **Ignore Leading Spaces**:
   - Skip over all leading spaces in the string.

2. **Check for an Optional Sign**:
   - Look for a `'+'` or `'-'` at the start of the number.

3. **Validate Digits and Decimal Points**:
   - Process digits before a decimal point.
   - Handle a decimal point and the digits after it (if present).

4. **Handle Scientific Notation**:
   - If an `'e'` or `'E'` is present, validate the part after it as an integer.

5. **Ignore Trailing Spaces**:
   - Skip over any trailing spaces.

6. **Final Validation**:
   - Ensure the entire string has been processed and contains at least one valid digit.

---

## Solution Code

```cpp
class Solution {
public:
    bool isNumber(string s) {
        int n = s.length();
        int i = 0;

        // Step 1: Ignore leading spaces
        while (i < n && isspace(s[i])) {
            i++;
        }

        // Step 2: Check for optional '+' or '-' sign
        if (i < n && (s[i] == '+' || s[i] == '-')) {
            i++;
        }

        bool hasDigits = false; // To track if at least one digit exists

        // Step 3: Process digits before a decimal point
        while (i < n && isdigit(s[i])) {
            hasDigits = true;
            i++;
        }

        // Step 4: Handle a decimal point and digits after it
        if (i < n && s[i] == '.') {
            i++; // Skip the '.'
            while (i < n && isdigit(s[i])) {
                hasDigits = true;
                i++;
            }
        }

        // Step 5: Process 'e' or 'E' for scientific notation
        if (hasDigits && i < n && (s[i] == 'e' || s[i] == 'E')) {
            i++; // Skip 'e' or 'E'
            hasDigits = false; // Reset, since we need digits after 'e'

            // Optional '+' or '-' sign after 'e'
            if (i < n && (s[i] == '+' || s[i] == '-')) {
                i++;
            }

            // Check digits in the exponent
            while (i < n && isdigit(s[i])) {
                hasDigits = true;
                i++;
            }
        }

        // Step 6: Ignore trailing spaces
        while (i < n && isspace(s[i])) {
            i++;
        }

        // Step 7: Valid if all characters processed and has valid digits
        return hasDigits && i == n;
    }
};
```

---

## Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the length of the string. We make a single pass through the string to validate it.
- **Space Complexity**: \(O(1)\), as no additional data structures are used.

---

## Edge Cases to Consider

1. Strings with only spaces, e.g., `"   "`.
2. Strings with just a decimal point, e.g., `"."`.
3. Strings with no digits after `'e'`, e.g., `"2e"`.
4. Strings with invalid characters, e.g., `"1a"`.

This implementation ensures all edge cases are handled properly!
