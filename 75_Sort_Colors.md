# 🟥🟦🟩 Problem Title: Sort Colors (0s, 1s, and 2s)

## Problem Statement

Given an array `nums` with elements 0, 1, and 2, the objective is to sort the array in-place so that all `0`s appear first, followed by `1`s, and then all `2`s. The algorithm should not use any built-in sort function and should aim for a simple solution with minimal extra space.

### Example

- **Input**: `nums = [2, 0, 2, 1, 1, 0]`  
  **Output**: `[0, 0, 1, 1, 2, 2]`

- **Input**: `nums = [2, 0, 1]`  
  **Output**: `[0, 1, 2]`

## Approach and Solution Explanation

To solve this problem, we use a **Bubble Sort** approach that repeatedly moves the largest unsorted element to its correct position in the array. Here’s a breakdown of the approach:

### Steps
1. **Initialize the Outer Loop**: We loop `n-1` times (where `n` is the size of `nums`), as each pass brings the next largest element to its final sorted position.
2. **Inner Loop for Comparison**: For each element, we compare it with the next element:
   - If `nums[j]` is greater than `nums[j + 1]`, we swap them, effectively moving larger elements to the right.
3. **Repeat**: After each outer loop iteration, the largest remaining unsorted element is placed in its correct position, sorting the array incrementally.

### Complexity Analysis
- **Time Complexity**: \(O(n^2)\), as the Bubble Sort algorithm uses nested loops that repeatedly traverse the list.
- **Space Complexity**: \(O(1)\), since the sorting is done in-place with no additional data structures.

### Solution Code

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int n = nums.size();

        for(int i = 1; i < n; i++) {
            // Perform the i-th pass
            for(int j = 0; j < n - 1; j++) {
                if(nums[j] > nums[j + 1]) {
                    swap(nums[j], nums[j + 1]);
                }
            }
        }
    }
};
```

## Edge Cases to Consider
- **All Same Element**: If `nums` contains only `0`s, `1`s, or `2`s, the function should return the array unchanged.
- **Already Sorted Array**: If `nums` is already sorted, the function should handle it without unnecessary swaps.
- **Empty Array**: If `nums` is empty, the function should handle it gracefully without errors.
- **Single Element Array**: For arrays of length 1, the array should be returned as-is.

## Alternative Efficient Solution
For optimal performance, consider **Dutch National Flag** algorithm for sorting in \(O(n)\) time complexity. This approach works by partitioning the array based on the values of 0, 1, and 2, ensuring all elements are sorted in one pass.
