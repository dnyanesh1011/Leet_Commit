# 🎢 Zigzag Conversion

## Problem Statement

Given a string `s` and an integer `numRows`, arrange the characters of `s` in a **zigzag pattern** on a given number of rows, and then read the characters line by line to produce the final string.

### Key Observations:
1. Characters are placed in a zigzag pattern across the rows.
2. The pattern moves **downwards** until the bottom row, then switches to **upwards** until the top row, and repeats.

---

## Examples

### Example 1:
**Input**:  
`s = "PAYPALISHIRING"`, `numRows = 3`  
**Output**:  
`"PAHNAPLSIIGYIR"`  

**Explanation**:
```
P   A   H   N
A P L S I I G
Y   I   R
```

---

### Example 2:
**Input**:  
`s = "PAYPALISHIRING"`, `numRows = 4`  
**Output**:  
`"PINALSIGYAHRPI"`  

**Explanation**:
```
P     I    N
A   L S  I G
Y A   H R
P     I
```

---

### Example 3:
**Input**:  
`s = "A"`, `numRows = 1`  
**Output**:  
`"A"`  

---

## Approach

1. **Handle Edge Cases**:
   - If `numRows == 1` or `s.length() <= numRows`, return `s` directly since zigzag is not applicable.

2. **Simulate Zigzag Row Placement**:
   - Use a vector of strings `rows` to simulate rows in the zigzag pattern.
   - Iterate through the characters of `s`:
     - Append each character to the current row.
     - Move **downwards** if at the top or **upwards** if at the bottom of the zigzag.

3. **Combine Rows**:
   - Concatenate all rows to form the resulting string.

---

## Solution Code

```cpp
class Solution {
public:
    string convert(string s, int numRows) {
        if (numRows == 1 || s.length() <= numRows) {
            return s; // No zigzag needed
        }

        vector<string> rows(min(numRows, (int)s.length())); // Create rows
        int currRow = 0; // Current row
        bool goingDown = false; // Direction flag

        for (char c : s) {
            rows[currRow] += c; // Add character to current row
            // Change direction at the top or bottom row
            if (currRow == 0 || currRow == numRows - 1) {
                goingDown = !goingDown;
            }
            // Move up or down
            currRow += goingDown ? 1 : -1;
        }

        // Combine all rows into a single string
        string result;
        for (const string& row : rows) {
            result += row;
        }
        return result;
    }
};
```

---

## Complexity Analysis

### Time Complexity:
- **O(n)**: Each character in `s` is processed exactly once.

### Space Complexity:
- **O(n)**: The `rows` vector stores up to `s.length()` characters.

---

## Edge Cases to Consider

1. **Single Row or Short String**:
   - Input: `s = "A"`, `numRows = 1`  
   - Output: `"A"`

2. **String Length Less Than Rows**:
   - Input: `s = "ABC"`, `numRows = 5`  
   - Output: `"ABC"`

3. **Multiple Full Zigzag Cycles**:
   - Input: `s = "PAYPALISHIRING"`, `numRows = 3`  
   - Output: `"PAHNAPLSIIGYIR"`

4. **No Zigzag Needed**:
   - Input: `s = "ZIGZAG"`, `numRows = 1`  
   - Output: `"ZIGZAG"`

---

This solution efficiently constructs the zigzag pattern and combines the rows to produce the desired output. 🌟
