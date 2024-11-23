# 🔍🏔️ Find Peak Element

## Problem Statement

Given an integer array `nums`, a peak element is an element that is **strictly greater** than its neighbors. You need to find and return the **index of any peak element**. 

A peak element satisfies the following condition:
- If `i` is a peak, then `nums[i] > nums[i - 1]` and `nums[i] > nums[i + 1]` (considering the boundaries of the array).

### Constraints:
- The array may contain multiple peaks.
- You may return the index of **any** peak, not necessarily the first or last one.
- The algorithm must run in **O(log n)** time complexity.

---

## Examples

### Example 1:
**Input:**  
`nums = [1, 2, 3, 1]`  
**Output:**  
`2`  
Explanation: The peak element is `3`, and its index is `2`.

### Example 2:
**Input:**  
`nums = [1, 2, 1, 3, 5, 6, 4]`  
**Output:**  
`5`  
Explanation: The peak element is `6`, and its index is `5`.  
Note: Another valid peak element is `2`, and its index is `1`.

---

## Approach and Solution Explanation

To solve this problem efficiently in **O(log n)** time complexity, we can utilize **binary search**. The idea behind the binary search approach is to compare the middle element with its neighbors and adjust the search bounds accordingly.

### Steps:
1. **Initialize the Boundaries**: Set `left` to `0` and `right` to `nums.size() - 1`.
2. **Binary Search**:
   - Calculate the `mid` index.
   - If `nums[mid] < nums[mid + 1]`, it indicates the peak element lies to the right of `mid`. Therefore, we move the `left` pointer to `mid + 1`.
   - Otherwise, if `nums[mid] >= nums[mid + 1]`, the peak might be at `mid` or to the left of `mid`. Therefore, we move the `right` pointer to `mid`.
3. **Termination**: The search continues until `left == right`, at which point we've found the peak element.

The binary search approach reduces the problem size by half at each step, ensuring a time complexity of **O(log n)**.

---

## Solution Code

```cpp
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        int left = 0, right = nums.size() - 1;
        
        while (left < right) {
            int mid = left + (right - left) / 2;
            
            // If the middle element is less than the next element, peak must be on the right side
            if (nums[mid] < nums[mid + 1]) {
                left = mid + 1;
            }
            // Otherwise, peak must be on the left side
            else {
                right = mid;
            }
        }
        
        // Left == right, a peak element is found
        return left;
    }
};
```

---

## Complexity Analysis

### Time Complexity:
- **Binary Search**: The algorithm performs binary search, reducing the search space by half at each iteration. Thus, the time complexity is **O(log n)**, where `n` is the size of the array.

### Space Complexity:
- **O(1)**: The algorithm only uses a few integer variables (`left`, `right`, `mid`) for the binary search process, so the space complexity is constant.

---

## Edge Cases to Consider

1. **Single Element**:
   - Input: `nums = [1]`
   - Output: `0` (A single element is always a peak by definition).

2. **All Elements in Decreasing Order**:
   - Input: `nums = [5, 4, 3, 2, 1]`
   - Output: `0` (The first element is the peak, since it is greater than its neighbors).

3. **All Elements in Increasing Order**:
   - Input: `nums = [1, 2, 3, 4, 5]`
   - Output: `4` (The last element is the peak, since it is greater than its neighbors).

4. **Multiple Peaks**:
   - Input: `nums = [1, 3, 2, 5, 4, 6]`
   - Output: `1` (The peak at index `1` with value `3` is a valid peak, or index `5` with value `6`).

5. **Array with Two Elements**:
   - Input: `nums = [1, 2]`
   - Output: `1` (The peak is the last element, as it is greater than its only neighbor).

---

## Conclusion

The **binary search** approach ensures that we can efficiently find a peak element in a sorted or unsorted array with **O(log n)** time complexity. This solution works for arrays of all sizes and handles different edge cases, such as arrays with one element, multiple peaks, and arrays with strictly increasing or decreasing values.
