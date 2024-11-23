# 📍 Search in Rotated Sorted Array

## Problem Statement

Given an integer array `nums` that is sorted in ascending order, the array is **possibly rotated** at an unknown pivot. You need to write a function to search for a given `target` in this rotated sorted array and return the index of the target. If the target is not found, return `-1`.

The array is rotated such that it is originally sorted in ascending order, but after a certain index `k`, the order is "shifted" so that the elements from `k` to the end come first, followed by elements from the beginning to `k-1`.

You must implement the algorithm with **O(log n)** time complexity.

### Constraints:
- The array will have distinct integers.
- The time complexity must be **O(log n)**.

---

## Examples

### Example 1:
**Input:**  
`nums = [4,5,6,7,0,1,2]`, `target = 0`  
**Output:**  
`4`  
Explanation: The target `0` is at index `4` in the rotated array.

### Example 2:
**Input:**  
`nums = [4,5,6,7,0,1,2]`, `target = 3`  
**Output:**  
`-1`  
Explanation: The target `3` is not present in the array.

### Example 3:
**Input:**  
`nums = [1]`, `target = 0`  
**Output:**  
`-1`  
Explanation: The target `0` is not present in the array.

---

## Approach and Solution Explanation

The key to solving this problem in **O(log n)** time complexity is to use **binary search**.

### Steps:
1. **Binary Search**: We can apply binary search to find the target in the rotated sorted array.
2. **Handling Rotation**: We need to determine which part of the array (left or right) is sorted at any point during the search and adjust the search space accordingly.
    - If `nums[left] <= nums[mid]`, it means the left part is sorted. We can check if the `target` lies within this sorted range.
    - If `nums[mid] <= nums[right]`, it means the right part is sorted. We can check if the `target` lies within this sorted range.

3. **Conditions**:
    - If the target is found at `nums[mid]`, return `mid`.
    - Otherwise, adjust the search range based on the comparisons and continue the search until the target is found or the search space is exhausted.

---

## Solution Code

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0, right = nums.size() - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] == target) {
                return mid; // target found
            }

            // Check if the left part is sorted
            if (nums[left] <= nums[mid]) {
                // If target is in the left part
                if (nums[left] <= target && target < nums[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            } else { // Right part is sorted
                // If target is in the right part
                if (nums[mid] < target && target <= nums[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }

        return -1; // Target not found
    }
};
```

---

## Complexity Analysis

### Time Complexity:
- **Binary Search**: Since we are reducing the search space by half in each iteration, the time complexity is **O(log n)**.

### Space Complexity:
- **O(1)**: The space complexity is constant since we are only using a few variables (`left`, `right`, `mid`) for the binary search process.

---

## Edge Cases to Consider

1. **Single Element Array**:
   - Input: `nums = [1]`, `target = 1`
   - Output: `0` (Element exists at index `0`).

2. **Array without Rotation**:
   - Input: `nums = [1, 2, 3, 4, 5]`, `target = 3`
   - Output: `2` (Array is not rotated, standard binary search works).

3. **Target Not Present**:
   - Input: `nums = [4, 5, 6, 7, 0, 1, 2]`, `target = 8`
   - Output: `-1` (Target is not present in the array).

4. **Array with Rotation at the End**:
   - Input: `nums = [3, 4, 5, 6, 7, 1, 2]`, `target = 1`
   - Output: `5` (Target `1` is found at index `5` after the rotation).

---

## Conclusion

This solution leverages binary search to find the target element in a rotated sorted array with an optimal time complexity of **O(log n)**. The approach handles rotation effectively by checking which part of the array is sorted in each step, ensuring that the search space is halved at each iteration.
