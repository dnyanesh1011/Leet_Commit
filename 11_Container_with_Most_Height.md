# 🫙Container With Most Water

## Problem Statement

Given an integer array `height` of length \( n \), where each element represents the height of a vertical line drawn at \( x \)-coordinate \( i \), find two lines that, together with the \( x \)-axis, form a container that holds the most water. Return the maximum amount of water the container can store. The container cannot be slanted.

---

## Examples

### Example 1:
**Input:**  
`height = [1,8,6,2,5,4,8,3,7]`  
**Output:**  
`49`  

**Explanation:**  
The two lines at positions 1 (height 8) and 8 (height 7) form a container with the largest area, given by:  
\[
\text{Area} = \text{min}(8, 7) \times (8 - 1) = 7 \times 7 = 49
\]

---

### Example 2:
**Input:**  
`height = [1,1]`  
**Output:**  
`1`  

**Explanation:**  
The only possible container is formed by the two lines, with area:  
\[
\text{Area} = \text{min}(1, 1) \times (1 - 0) = 1
\]

---

## Approach

### Two-Pointer Technique:

1. **Initialize Two Pointers**:
   - Start with one pointer at the leftmost position (`left = 0`) and the other at the rightmost position (`right = n - 1`).

2. **Calculate Area**:
   - Compute the area between the two lines using the formula:  
     \[
     \text{Area} = \text{min}(\text{height}[left], \text{height}[right]) \times (\text{right} - \text{left})
     \]

3. **Update Maximum Area**:
   - Track the maximum area encountered during the iterations.

4. **Move the Pointer with Smaller Height**:
   - To potentially find a larger area, move the pointer corresponding to the smaller height inward.

5. **Repeat Until Pointers Meet**:
   - Continue the process until `left` equals `right`.

---

## Solution Code

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int left = 0, right = height.size() - 1;
        int maxArea = 0;

        while (left < right) {
            // Calculate the area between the two pointers
            int currentArea = min(height[left], height[right]) * (right - left);
            maxArea = max(maxArea, currentArea);

            // Move the pointer with the smaller height
            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }

        return maxArea;
    }
};
```

---

## Complexity Analysis

### Time Complexity:
- **O(n)**:  
  The two-pointer approach ensures that each pointer is moved at most \( n \) times.

### Space Complexity:
- **O(1)**:  
  The solution uses a constant amount of additional space.

---

## Edge Cases to Consider

1. **Minimum Input Size**:
   - Input: `height = [1,2]`  
   - Output: `1`  

2. **All Heights Equal**:
   - Input: `height = [5,5,5,5,5]`  
   - Output: \( 5 \times (\text{length} - 1) \).  

3. **Decreasing Heights**:
   - Input: `height = [5,4,3,2,1]`  
   - Output: Determined by the first and last elements.  

4. **Empty or Single Element**:
   - Input: `height = []` or `height = [1]`  
   - Output: Not valid as per constraints (array length \( \geq 2 \)).

---

## Notes

This solution effectively finds the container with the maximum area using a greedy two-pointer strategy. By iterating from both ends, it avoids a brute-force \( O(n^2) \) approach and ensures efficiency. 🚀
