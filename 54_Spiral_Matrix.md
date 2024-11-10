# 🔄 Spiral Matrix Traversal

## Problem Statement
Given a 2D matrix, return all elements of the matrix in spiral order, moving layer by layer from the outermost elements towards the center.

### Example
**Input:**
```cpp
matrix = [
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
```

**Output:**
```cpp
[1, 2, 3, 6, 9, 8, 7, 4, 5]
```

**Explanation:**
The elements are added in a spiral order: start from the top left, traverse the top row, then the right column, bottom row, and finally the left column, moving inward after each complete loop.

## Approach and Solution Explanation

### Boundary-Controlled Traversal
The solution uses boundaries (`startingRow`, `endingRow`, `startingCol`, and `endingCol`) to define the limits for each layer of the matrix. These boundaries are progressively moved inward until all elements have been visited.

1. **Initialize Boundaries and Counters**:
   - Define starting and ending indices for rows and columns.
   - Track the total elements and a counter `count` to ensure all elements are processed.

2. **Traverse in Four Steps**:
   - **Top Row**: Traverse from left to right across the topmost row.
   - **Right Column**: Traverse downward along the rightmost column.
   - **Bottom Row**: Traverse from right to left along the bottom row (only if not already traversed).
   - **Left Column**: Traverse upward along the leftmost column (only if not already traversed).

3. **Update Boundaries**:
   - After each traversal step, adjust the relevant boundary inward to avoid revisiting elements.

4. **Loop Until All Elements Are Processed**:
   - Repeat the traversal steps while `count` is less than the total number of elements.

### Complexity Analysis
- **Time Complexity**: \(O(m \times n)\), where \(m\) is the number of rows and \(n\) is the number of columns, as each element is visited exactly once.
- **Space Complexity**: \(O(1)\) extra space (ignoring the output vector `ans`), since the traversal is performed in-place without additional data structures.

## Solution Code
```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> ans;
        
        // Check if the matrix is empty
        if (matrix.empty()) return ans;
        
        int row = matrix.size();
        int col = matrix[0].size();

        int count = 0;
        int total = row * col;

        // Index initialization
        int startingRow = 0;
        int startingCol = 0;
        int endingRow = row - 1;
        int endingCol = col - 1;

        while (count < total) {
            // Traverse starting row
            if (count < total) {
                for (int index = startingCol; index <= endingCol; index++) {
                    ans.push_back(matrix[startingRow][index]);
                    count++;
                }
                startingRow++;
            }

            // Traverse ending column
            if (count < total) {
                for (int index = startingRow; index <= endingRow; index++) {
                    ans.push_back(matrix[index][endingCol]);
                    count++;
                }
                endingCol--;
            }

            // Traverse ending row
            if (count < total) {
                for (int index = endingCol; index >= startingCol; index--) {
                    ans.push_back(matrix[endingRow][index]);
                    count++;
                }
                endingRow--;
            }

            // Traverse starting column
            if (count < total) {
                for (int index = endingRow; index >= startingRow; index--) {
                    ans.push_back(matrix[index][startingCol]);
                    count++;
                }
                startingCol++;
            }
        }
        return ans;
    }
};
```

## Edge Cases to Consider
- **Empty Matrix**: If the matrix is empty, the function should return an empty result.
- **Single Row or Column**: The function should correctly handle matrices with only one row or one column.
- **Square Matrix**: Handles a square matrix of any size.
- **Non-Square Matrix**: Correctly processes matrices with differing numbers of rows and columns.
- **One Element Matrix**: Should return the single element in the matrix without errors. 

This approach ensures the function can handle various matrix configurations in an efficient and organized manner.
