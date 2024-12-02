# Rotate Image 🔄

## Problem Description

You are given an \(n \times n\) 2D matrix that represents an image. The goal is to **rotate the image by 90 degrees clockwise** **in-place**.  
This means you must modify the input matrix directly without allocating a new 2D matrix.

---

## Examples

### Example 1

**Input**:  
```plaintext
matrix = [[1, 2, 3],
          [4, 5, 6],
          [7, 8, 9]]
```  
**Output**:  
```plaintext
[[7, 4, 1],
 [8, 5, 2],
 [9, 6, 3]]
```  

---

### Example 2

**Input**:  
```plaintext
matrix = [[5, 1, 9, 11],
          [2, 4, 8, 10],
          [13, 3, 6, 7],
          [15, 14, 12, 16]]
```  
**Output**:  
```plaintext
[[15, 13, 2, 5],
 [14, 3, 4, 1],
 [12, 6, 8, 9],
 [16, 7, 10, 11]]
```

---

## Approach and Solution Explanation

### Key Insights

1. **Transpose the Matrix**:  
   - Convert all rows into columns by swapping the elements across the diagonal (\(i, j \leftrightarrow j, i\)).
   
2. **Reverse Each Row**:  
   - After transposing, reverse the order of elements in each row to achieve a 90-degree clockwise rotation.

---

### Algorithm Steps

1. **Transpose the Matrix**:
   - Iterate through the upper triangular part of the matrix.
   - Swap \( \text{matrix}[i][j] \) with \( \text{matrix}[j][i] \).

2. **Reverse Each Row**:
   - For every row in the matrix, reverse the elements.

3. **In-Place Modification**:
   - All operations are performed directly on the input matrix without extra space.

---

### Complexity Analysis

1. **Time Complexity**:  
   - Transposing takes \(O(n^2)\), where \(n\) is the size of the matrix.  
   - Reversing each row takes \(O(n^2)\).  
   **Total**: \(O(n^2)\).

2. **Space Complexity**:  
   - \(O(1)\): In-place modification without additional storage.

---

## Solution Code

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();

        // Step 1: Transpose the matrix
        for (int i = 0; i < n; ++i) {
            for (int j = i + 1; j < n; ++j) {
                swap(matrix[i][j], matrix[j][i]);
            }
        }

        // Step 2: Reverse each row
        for (int i = 0; i < n; ++i) {
            reverse(matrix[i].begin(), matrix[i].end());
        }
    }
};
```

---

## Example Walkthrough

### Input:  
```plaintext
matrix = [[1, 2, 3],
          [4, 5, 6],
          [7, 8, 9]]
```

### Step 1: Transpose the Matrix  
After swapping elements across the diagonal:  
```plaintext
[[1, 4, 7],
 [2, 5, 8],
 [3, 6, 9]]
```

### Step 2: Reverse Each Row  
After reversing rows:  
```plaintext
[[7, 4, 1],
 [8, 5, 2],
 [9, 6, 3]]
```

**Output**:  
```plaintext
[[7, 4, 1],
 [8, 5, 2],
 [9, 6, 3]]
```

---

## Edge Cases

1. **Single Element Matrix**:  
   - Input: `matrix = [[1]]`  
   - Output: `[[1]]` (No change).  

2. **Two-by-Two Matrix**:  
   - Input: `matrix = [[1, 2], [3, 4]]`  
   - Output: `[[3, 1], [4, 2]]`.  

3. **Empty Matrix**:  
   - Input: `matrix = []`  
   - Output: `[]`.

---

## Key Notes

- **Transpose + Reverse** is an efficient and intuitive way to perform in-place 90-degree rotations.
- Works for any square matrix size \(n \times n\).
