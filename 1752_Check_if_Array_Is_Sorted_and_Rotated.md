# 📝 Check if Array is Sorted and Rotated

## Problem Overview

The problem requires determining if a given array, `nums`, was originally sorted in non-decreasing order and then rotated some number of times (including zero rotations). The array may contain duplicates. We return `true` if `nums` could represent a sorted and rotated array, and `false` otherwise.

### Example
- **Input**: `nums = [3, 4, 5, 1, 2]`  
  **Output**: `true`  
  **Explanation**: `[1, 2, 3, 4, 5]` is the original sorted array. Rotating by 3 positions yields `[3, 4, 5, 1, 2]`.

- **Input**: `nums = [2, 1, 3, 4]`  
  **Output**: `false`  
  **Explanation**: There’s no rotation of a sorted array that matches `nums`.

## Approach and Solution Explanation

The solution uses a **single-pass check** to count any "breakpoints" in the array—places where an element is greater than the next element. In a valid sorted-then-rotated array:
- There should be **at most one breakpoint**.
- Additionally, the last element should not be greater than the first, unless the rotation starts from the beginning.

### Steps
1. Traverse the array once, counting the number of times an element is greater than its next neighbor.
2. Check if the last element is greater than the first element, as this can indicate an additional breakpoint.
3. If the total breakpoints (transitions) are zero or one, the array is considered sorted and rotated.

### Complexity Analysis
- **Time Complexity**: \(O(n)\), where \(n\) is the number of elements in `nums`, because we only iterate through the array once.
- **Space Complexity**: \(O(1)\), as we only use a fixed amount of space to store the `count` of breakpoints.

## Solution Code

```cpp
class Solution {
public:
    bool check(vector<int>& nums) {
        int n = nums.size();
        int count = 0;

        // Check for breakpoints in the array
        for (int i = 1; i < n; i++)
            if (nums[i - 1] > nums[i])
                count++;

        // Check if the last element > first element, adding an additional breakpoint
        if (nums[n - 1] > nums[0])
            count++;

        // Return true if there’s at most one breakpoint
        return count <= 1;
    }
};
```
