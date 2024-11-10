# 🗃️ Remove Duplicates from Sorted Array

## Problem Statement
Given a sorted integer array `nums`, remove the duplicates in-place such that each unique element appears only once. The function should return the number of unique elements, `k`, where the first `k` elements of `nums` contain the unique elements in their original order. The remaining elements in the array beyond `k` are not important.

### Example
**Input:**
```cpp
nums = [1, 1, 2]
```

**Output:**
```cpp
2, nums = [1, 2, _]
```

**Explanation:** 
The function should return `k = 2`, with the first two elements of `nums` being `1` and `2`, respectively. It doesn’t matter what values are beyond the first `k` elements, as they are not part of the required output.

## Approach and Solution Explanation

### Two-Pointer Technique
This solution uses a two-pointer technique to efficiently modify `nums` in-place.

1. **Two Pointers**:
   - A slow pointer `i` that tracks the position for placing unique elements.
   - A fast pointer `j` that scans through each element in the array, starting from index `1`.

2. **Loop and Check for Uniqueness**:
   - If `nums[j]` is not equal to `nums[i]` (indicating a unique element), increment `i` and place `nums[j]` at `nums[i]`.
   - Continue until all elements are processed.

3. **Return Result**:
   - After the loop, `i + 1` represents the number of unique elements in the array.

### Complexity Analysis
- **Time Complexity**: \(O(n)\), where \(n\) is the number of elements in `nums`, as we traverse the array once.
- **Space Complexity**: \(O(1)\), as the function modifies `nums` in-place without using additional data structures.

## Solution Code
```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.empty()) return 0; // Handle empty array case

        int i = 0; // Initialize slow pointer
        for (int j = 1; j < nums.size(); j++) { // Start fast pointer from 1
            if (nums[j] != nums[i]) { // Check if current element is unique
                i++; // Move slow pointer
                nums[i] = nums[j]; // Place unique element at position i
            }
        }
        return i + 1; // i+1 is the count of unique elements
    }
};
```

## Edge Cases to Consider
- **Empty Array**: If `nums` is empty, the function should return `0`.
- **No Duplicates**: If all elements in `nums` are unique, the function should return the size of `nums`.
- **All Duplicates**: If all elements in `nums` are the same, the function should return `1`.
- **Single Element Array**: For arrays with only one element, the function should return `1`.

