# 📍 Find First and Last Position of Element in Sorted Array

## Problem Statement

Given a sorted array `nums` and a target value, the goal is to find the **starting** and **ending** positions of a given target value. If the target is not found in the array, return `[-1, -1]`.

The array is sorted in non-decreasing order, and the target may appear one or more times.

The algorithm should run in **O(log n)** time complexity.

### Constraints:
- The array `nums` is sorted in non-decreasing order.
- The array may contain duplicates of the target value.
- The time complexity must be **O(log n)**.

---

## Examples

### Example 1:
**Input:**  
`nums = [5,7,7,8,8,10]`, `target = 8`  
**Output:**  
`[3, 4]`  
Explanation: The target `8` first appears at index `3` and last appears at index `4`.

### Example 2:
**Input:**  
`nums = [5,7,7,8,8,10]`, `target = 6`  
**Output:**  
`[-1, -1]`  
Explanation: The target `6` is not present in the array.

### Example 3:
**Input:**  
`nums = []`, `target = 0`  
**Output:**  
`[-1, -1]`  
Explanation: The array is empty, so no target exists.

---

## Approach and Solution Explanation

To achieve the required **O(log n)** time complexity, we use **binary search**. The main idea is to use binary search twice:
1. **First Search**: Find the first occurrence of the target.
2. **Second Search**: Find the last occurrence of the target.

### Steps:
1. **Find the First Occurrence**:
   - Perform a binary search where, if the middle element is equal to the target, we continue searching on the left side (because we want the first occurrence).
2. **Find the Last Occurrence**:
   - Perform a binary search where, if the middle element is equal to the target, we continue searching on the right side (because we want the last occurrence).

The `findBound` function is responsible for performing the binary search, and it is called twice: once for the first occurrence and once for the last occurrence.

---

## Solution Code

```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> result = {-1, -1};
        
        // Find the first position of the target
        result[0] = findBound(nums, target, true);
        if (result[0] == -1) {
            return result;  // If the target is not found
        }
        
        // Find the last position of the target
        result[1] = findBound(nums, target, false);
        
        return result;
    }

private:
    int findBound(const vector<int>& nums, int target, bool isFirst) {
        int left = 0, right = nums.size() - 1;
        int bound = -1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (nums[mid] == target) {
                bound = mid;
                if (isFirst) {
                    right = mid - 1;  // Search left side for the first occurrence 
                } else {
                    left = mid + 1;   // Search right side for the last occurrence
                }
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return bound;
    }
};
```

---

## Complexity Analysis

### Time Complexity:
- **Binary Search**: Each call to `findBound` takes **O(log n)** time due to the binary search.
- We call `findBound` twice (once for the first occurrence and once for the last), so the overall time complexity is **O(log n)**.

### Space Complexity:
- **O(1)**: We only use a few integer variables for the binary search (`left`, `right`, `mid`, and `bound`) and the result array.

---

## Edge Cases to Consider

1. **Target not present**:
   - Input: `nums = [1, 2, 3, 4, 5]`, `target = 6`
   - Output: `[-1, -1]` (Target is not found in the array).

2. **Target appears once**:
   - Input: `nums = [1, 2, 3, 4, 5]`, `target = 3`
   - Output: `[2, 2]` (Target is found at index `2`).

3. **Target appears multiple times**:
   - Input: `nums = [1, 2, 2, 2, 3, 4, 5]`, `target = 2`
   - Output: `[1, 3]` (Target `2` first appears at index `1` and last appears at index `3`).

4. **Empty array**:
   - Input: `nums = []`, `target = 3`
   - Output: `[-1, -1]` (The array is empty, so no target can be found).

5. **Target is at the bounds**:
   - Input: `nums = [1, 2, 3, 4, 5]`, `target = 1`
   - Output: `[0, 0]` (Target `1` is found at index `0`).

---

## Conclusion

This solution efficiently finds the first and last positions of a target element in a sorted array using binary search. By performing binary search twice, we ensure that the time complexity remains **O(log n)**, meeting the problem's requirements. The approach handles edge cases, such as an empty array or a target not present in the array, effectively.
