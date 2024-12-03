# ♟️♟️ N-Queens II Problem

## Problem Overview

The **N-Queens II** problem is a variation of the classic **N-Queens** puzzle:
1. You must place `n` queens on an `n x n` chessboard.
2. No two queens can attack each other (i.e., no two queens can share the same row, column, or diagonal).
3. Instead of returning all valid configurations, this problem requires **only the count of distinct solutions**.

---

## Examples

### Example 1
**Input**:  
```plaintext
n = 4
```

**Output**:  
```plaintext
2
```

**Explanation**:  
There are exactly **two distinct solutions** to the 4-Queens problem.

### Example 2
**Input**:  
```plaintext
n = 1
```

**Output**:  
```plaintext
1
```

**Explanation**:  
For a 1x1 chessboard, there is only one valid solution.

---

## Approach and Solution Explanation

This problem can be solved using **backtracking**. Instead of storing and returning all configurations like in the classic N-Queens problem, we maintain a **counter** to track the number of valid solutions.

### Steps
1. **Backtracking**:
   - Start placing queens row by row.
   - For each row:
     - Try placing a queen in every column.
     - Check if the placement is valid:
       - No queens should exist in the same column.
       - No queens should exist in the same diagonal (both top-left to bottom-right and top-right to bottom-left).
     - If valid, recursively move to the next row.
   - If all rows are successfully filled, increment the solution counter.

2. **Validation**:
   - Use arrays or bit manipulation to efficiently check and track:
     - Columns occupied by queens.
     - Occupied diagonals.

---

### Complexity Analysis

- **Time Complexity**:  
  - Worst-case: \(O(N!)\), where \(N\) is the size of the chessboard. The number of valid configurations reduces the search space.
- **Space Complexity**:  
  - \(O(N)\) for recursion stack and tracking arrays.

---

## Solution Code

```cpp
class Solution {
public:
    int totalNQueens(int n) {
        int count = 0;
        vector<bool> columns(n, false);
        vector<bool> diag1(2 * n - 1, false); // Top-left to bottom-right diagonal
        vector<bool> diag2(2 * n - 1, false); // Top-right to bottom-left diagonal
        backtrack(0, n, columns, diag1, diag2, count);
        return count;
    }

private:
    void backtrack(int row, int n, vector<bool>& columns, vector<bool>& diag1, vector<bool>& diag2, int& count) {
        if (row == n) {
            count++;
            return;
        }
        for (int col = 0; col < n; ++col) {
            if (columns[col] || diag1[row - col + n - 1] || diag2[row + col]) continue;
            columns[col] = diag1[row - col + n - 1] = diag2[row + col] = true;
            backtrack(row + 1, n, columns, diag1, diag2, count);
            columns[col] = diag1[row - col + n - 1] = diag2[row + col] = false;
        }
    }
};
```

---

## Example Walkthrough

### Input: `n = 4`

#### Backtracking Steps:
1. Place a queen in row 1 at a valid column.
2. Recursively attempt to place queens in subsequent rows.
3. If all rows are successfully filled, increment the solution counter.
4. Backtrack to explore other valid configurations.

#### Output:
```plaintext
2
```

---

## Edge Cases

1. **Smallest Board**:  
   - Input: `n = 1`.  
     Output: `1`.

2. **Impossible Board**:  
   - Input: `n = 2` or `n = 3`.  
     Output: `0`.

3. **Performance**:  
   - For larger values of `n` (e.g., `n = 10`), ensure the solution runs efficiently.

---

## Summary

The **N-Queens II** problem focuses on counting valid solutions rather than generating them. Using **backtracking** with efficient pruning techniques ensures that only valid configurations are explored, minimizing computational overhead.
