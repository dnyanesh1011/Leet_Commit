# Spiral Matrix II

## Problem Statement

Given a positive integer `n`, generate an \( n \times n \) matrix filled with elements from `1` to \( n^2 \) in spiral order.

---

## Examples

### Example 1
**Input:**  
`n = 3`  
**Output:**  
`[[1,2,3],[8,9,4],[7,6,5]]`  

---

### Example 2
**Input:**  
`n = 1`  
**Output:**  
`[[1]]`  

---

## Approach

To generate the spiral matrix:
1. **Use Boundaries**:  
   Define four boundaries (`top`, `bottom`, `left`, and `right`) to control the direction of traversal.

2. **Traverse in a Spiral Order**:  
   - Move **left to right** across the top boundary.
   - Move **top to bottom** along the right boundary.
   - Move **right to left** along the bottom boundary.
   - Move **bottom to top** along the left boundary.

3. **Fill Numbers Sequentially**:  
   Incrementally fill numbers while adjusting boundaries after each traversal.

4. **Stop Condition**:  
   The traversal stops when all elements are filled.

---

## Solution Code

```cpp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> matrix(n, vector<int>(n, 0)); // Initialize matrix
        int top = 0, bottom = n - 1, left = 0, right = n - 1;
        int num = 1; // Start filling from 1

        while (top <= bottom && left <= right) {
            // Fill the top row
            for (int i = left; i <= right; ++i) {
                matrix[top][i] = num++;
            }
            ++top; // Move top boundary down

            // Fill the right column
            for (int i = top; i <= bottom; ++i) {
                matrix[i][right] = num++;
            }
            --right; // Move right boundary left

            // Fill the bottom row (if within bounds)
            if (top <= bottom) {
                for (int i = right; i >= left; --i) {
                    matrix[bottom][i] = num++;
                }
                --bottom; // Move bottom boundary up
            }

            // Fill the left column (if within bounds)
            if (left <= right) {
                for (int i = bottom; i >= top; --i) {
                    matrix[i][left] = num++;
                }
                ++left; // Move left boundary right
            }
        }

        return matrix;
    }
};
```

---

## Complexity Analysis

### Time Complexity:
- **O(n²)**:  
  Each element in the \( n \times n \) matrix is visited exactly once.

### Space Complexity:
- **O(1)**:  
  Aside from the output matrix, no additional space is used.

---

## Explanation of Example 1

**Input:** `n = 3`  

1. Initialize `matrix = [[0,0,0], [0,0,0], [0,0,0]]`.  
2. Traverse and fill:  
   - Top row → `[1,2,3]`  
   - Right column → `[4,5]`  
   - Bottom row → `[6,7]` (reversed)  
   - Left column → `[8]`  
   - Center → `[9]`  

**Output:** `[[1,2,3],[8,9,4],[7,6,5]]`  

---

This approach ensures a clean, systematic traversal while maintaining clarity and efficiency.
