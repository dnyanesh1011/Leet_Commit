# ♟️ N-Queens Problem

## Problem Overview

The **N-Queens** puzzle involves placing `n` queens on an `n x n` chessboard such that:
1. No two queens attack each other.
   - Queens attack each other if they are on the same row, column, or diagonal.
2. You must return all possible distinct solutions.

Each solution is represented as a chessboard configuration, where:
- `'Q'` represents a queen.
- `'.'` represents an empty space.

---

## Examples

### Example 1
**Input**:  
```plaintext
n = 4
```

**Output**:  
```plaintext
[
 [".Q..",  // Q at row 1, column 2
  "...Q",  // Q at row 2, column 4
  "Q...",  // Q at row 3, column 1
  "..Q."], // Q at row 4, column 3

 ["..Q.",  // Q at row 1, column 3
  "Q...",  // Q at row 2, column 1
  "...Q",  // Q at row 3, column 4
  ".Q.."]  // Q at row 4, column 2
]
```

**Explanation**:  
There are **two distinct solutions** for the 4-Queens problem.

---

### Example 2
**Input**:  
```plaintext
n = 1
```

**Output**:  
```plaintext
[["Q"]]
```

**Explanation**:  
A single queen on a 1x1 chessboard is the only valid solution.

---

## Approach and Solution Explanation

### Insight

The problem can be solved using **backtracking**, where:
- We recursively explore all potential queen placements.
- At each step:
  - Check if placing a queen at a given position is valid.
  - If valid, move to the next row.
  - If not, backtrack and try a different placement.

---

### Steps

1. **Initialize the Chessboard**:
   - Use a 2D array or a list of strings to represent the board.

2. **Backtracking**:
   - Place one queen per row.
   - For each row:
     - Iterate through all columns.
     - Check if placing a queen at `(row, col)` is valid.
     - If valid:
       - Place the queen and move to the next row.
       - If all rows are filled, store the solution.
     - Backtrack by removing the queen and trying the next position.

3. **Validation**:
   - Ensure no queen exists in:
     - The same column.
     - The top-left to bottom-right diagonal.
     - The top-right to bottom-left diagonal.

---

### Complexity Analysis

- **Time Complexity**:  
  - \(O(N!)\): Each row has \(N\) choices, reducing as we go deeper.
- **Space Complexity**:  
  - \(O(N^2)\): Space required to store the board and recursive stack.

---

## Solution Code

```cpp
class Solution {
public:
    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> solutions;
        vector<string> board(n, string(n, '.'));
        backtrack(0, n, board, solutions);
        return solutions;
    }

private:
    void backtrack(int row, int n, vector<string>& board, vector<vector<string>>& solutions) {
        if (row == n) {
            solutions.push_back(board);
            return;
        }
        for (int col = 0; col < n; ++col) {
            if (isValid(row, col, n, board)) {
                board[row][col] = 'Q';
                backtrack(row + 1, n, board, solutions);
                board[row][col] = '.'; // Backtrack
            }
        }
    }

    bool isValid(int row, int col, int n, vector<string>& board) {
        // Check column
        for (int i = 0; i < row; ++i)
            if (board[i][col] == 'Q') return false;

        // Check top-left diagonal
        for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; --i, --j)
            if (board[i][j] == 'Q') return false;

        // Check top-right diagonal
        for (int i = row - 1, j = col + 1; i >= 0 && j < n; --i, ++j)
            if (board[i][j] == 'Q') return false;

        return true;
    }
};
```

---

## Example Walkthrough

### Input: `n = 4`

#### Backtracking Steps:
1. Place Q at `(1,1)`.  
2. Place Q at `(2,3)`.  
3. Place Q at `(3,4)`.  
4. Backtrack when no valid position exists for row 4.  
5. Explore all other possibilities.  

#### Output:
```plaintext
[
 [".Q..", "...Q", "Q...", "..Q."],
 ["..Q.", "Q...", "...Q", ".Q.."]
]
```

---

## Edge Cases

1. **Smallest Board**:  
   - Input: `n = 1`.  
     Output: `[["Q"]]`.

2. **No Solution**:
   - Input: `n = 2` or `n = 3`.  
     Output: `[]`.

3. **Larger Boards**:
   - Input: `n > 4`.  
     Test for performance and correctness.

---

## Summary

The N-Queens problem is a classic **backtracking** problem. This approach ensures that all valid configurations are explored systematically while eliminating invalid configurations early.
