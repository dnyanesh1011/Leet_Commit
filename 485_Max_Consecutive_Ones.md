# 🟰🟰 Problem Title: Max Consecutive Ones

## Problem Statement
Given a binary array `nums`, the goal is to find the maximum number of consecutive `1`s in the array. Return this maximum count.

### Example
- **Input**: `nums = [1,1,0,1,1,1]`  
  **Output**: `3`  
  **Explanation**: The maximum number of consecutive `1`s is 3 (the last three elements).

- **Input**: `nums = [1,0,1,1,0,1]`  
  **Output**: `2`  
  **Explanation**: The maximum number of consecutive `1`s is 2.

## Approach and Solution Explanation

To solve this problem, we can iterate through the array while tracking two variables:
1. **`currentCount`**: Counts the current sequence of consecutive `1`s.
2. **`maxCount`**: Tracks the maximum number of consecutive `1`s encountered so far.

### Steps
1. **Initialize Counters**: Start `maxCount` and `currentCount` at 0.
2. **Iterate Through `nums`**:
   - If the current element is `1`, increase `currentCount`.
   - If the current element is `0`, compare `currentCount` with `maxCount` and update `maxCount` if `currentCount` is greater. Then reset `currentCount` to 0.
3. **Final Check**: After the loop, update `maxCount` one last time in case the longest sequence of `1`s is at the end of the array.
4. **Return** `maxCount` as the result.

### Complexity Analysis
- **Time Complexity**: \(O(n)\), where \(n\) is the length of `nums`, since we only need one pass through the array.
- **Space Complexity**: \(O(1)\), as we only use a fixed amount of additional space for tracking counters.

## Solution Code

```cpp
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int maxCount = 0; 
        int currentCount = 0;

        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] == 1) {
                currentCount++;
            } else {
                maxCount = max(maxCount, currentCount);
                currentCount = 0;
            }
        }
        
        return max(maxCount, currentCount); // Final check for last sequence of consecutive 1s
    }
};
```

## Edge Cases to Consider
- **All Zeros**: If `nums` contains only `0`s, the function should return `0`.
- **All Ones**: If `nums` is composed entirely of `1`s, `maxCount` should equal the length of `nums`.
- **Single Element Array**: The function should handle both `[1]` and `[0]` correctly.
- **Trailing Ones**: If the longest sequence of `1`s is at the end, the function should still capture this in the final result.
