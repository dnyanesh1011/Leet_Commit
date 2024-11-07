# 🔄 Rotate Array

## Problem Overview

Given an integer array `nums`, the goal is to rotate the array to the right by `k` steps, where `k` is a non-negative integer. The solution must be done **in-place** with **O(1)** extra space.

### Examples

- **Example 1**  
  **Input**: `nums = [1,2,3,4,5,6,7]`, `k = 3`  
  **Output**: `[5,6,7,1,2,3,4]`  
  **Explanation**:  
    - Rotate 1 step: `[7,1,2,3,4,5,6]`
    - Rotate 2 steps: `[6,7,1,2,3,4,5]`
    - Rotate 3 steps: `[5,6,7,1,2,3,4]`
  
- **Example 2**  
  **Input**: `nums = [-1,-100,3,99]`, `k = 2`  
  **Output**: `[3,99,-1,-100]`  
  **Explanation**:  
    - Rotate 1 step: `[99,-1,-100,3]`
    - Rotate 2 steps: `[3,99,-1,-100]`

## Approach and Solution Explanation

The solution uses a **reversal technique** to rotate the array efficiently. Here's a step-by-step breakdown of the approach:

### Steps
1. **Modulo Operation**: 
   Since rotating by the length of the array or any multiple of it returns the original array, we reduce `k` by taking `k % n` where `n` is the length of the array.

2. **Reverse Entire Array**:  
   By reversing the entire array, the elements move to the opposite ends.

3. **Reverse First k Elements**:  
   The first `k` elements (now at the end of the rotated array) are reversed to restore their correct order in the rotated array.

4. **Reverse Remaining Elements**:  
   Finally, reverse the remaining `n - k` elements to restore their order.

### Complexity Analysis
- **Time Complexity**: \(O(n)\), where \(n\) is the number of elements in `nums`, since we reverse the array in-place three times.
- **Space Complexity**: \(O(1)\), as we perform the rotation in-place without additional data structures.

## Solution Code

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        k %= n;  // Handle cases where k >= n
        
        // Step 1: Reverse the entire array
        reverse(nums.begin(), nums.end());
        
        // Step 2: Reverse the first k elements
        reverse(nums.begin(), nums.begin() + k);
        
        // Step 3: Reverse the remaining n - k elements
        reverse(nums.begin() + k, nums.end());
    }
};
```

## Conclusion

This solution efficiently rotates the array in-place with a time complexity of \(O(n)\) and no extra space usage, making it optimal for large arrays. The reversal technique is a simple yet effective approach to rotating arrays without the need for additional storage or complex operations.
