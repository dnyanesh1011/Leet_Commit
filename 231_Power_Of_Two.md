# 🌀Zigzag Conversion

## Problem Statement

Given a string `s` and a number `numRows`, rearrange the string in a zigzag pattern on a given number of rows, as shown in the example below, and then read it line by line.

---

### Example:

#### Input:  
`PAYPALISHIRING`, `numRows = 3`

#### Output:  
`PAHNAPLSIIGYIR`

#### Explanation:  
The zigzag pattern:

```
P   A   H   N
A P L S I I G
Y   I   R
```

---

#### Input:  
`PAYPALISHIRING`, `numRows = 4`

#### Output:  
`PINALSIGYAHRPI`

#### Explanation:
The zigzag pattern:

```
P     I    N
A   L S  I G
Y A   H R
P     I
```

#### Input:
`s = "A"`, `numRows = 1`

#### Output:
`"A"`

---

## Approach

This problem requires simulating the zigzag pattern and then reconstructing the string. Below are the steps to solve it:

1. **Edge Cases**:
   - If `numRows == 1` or the string's length is less than or equal to `numRows`, return the string as is. No zigzag pattern is needed.

2. **Simulate Zigzag**:
   - Use a `vector<string>` to represent rows.
   - Traverse the string and append characters to the appropriate row, alternating direction (up/down) when the top or bottom is reached.

3. **Combine Rows**:
   - Concatenate all rows to form the final string.

---

## Solution Code

### **C++ Implementation**

```cpp
#include <string>
#include <vector>
using namespace std;

class Solution {
public:
    string convert(string s, int numRows) {
        if (numRows == 1 || s.length() <= numRows) {
            return s; // No zigzag pattern needed
        }

        vector<string> rows(min(numRows, (int)s.length()));
        int currRow = 0;
        bool goingDown = false;

        for (char c : s) {
            rows[currRow] += c; // Append the character to the current row
            // Change direction at the top or bottom
            if (currRow == 0 || currRow == numRows - 1) {
                goingDown = !goingDown;
            }
            currRow += goingDown ? 1 : -1; // Move up or down
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
- \(O(n)\), where \(n\) is the length of the input string. Each character is processed once.

### Space Complexity:
- \(O(n)\), for storing rows in the `vector<string>`.

---

## Edge Cases to Consider:

1. **Single Row**:
   - Input: `s = "HelloWorld"`, `numRows = 1`
   - Output: `"HelloWorld"`

2. **Input Length <= numRows**:
   - Input: `s = "Hi"`, `numRows = 5`
   - Output: `"Hi"`

3. **Already Balanced Pattern**:
   - Input: `s = "A"`, `numRows = 1`
   - Output: `"A"`

4. **Normal Pattern**:
   - Input: `"PAYPALISHIRING"`, `numRows = 3`
   - Output: `"PAHNAPLSIIGYIR"`

--- 

This solution ensures an efficient and correct zigzag conversion of the string.
