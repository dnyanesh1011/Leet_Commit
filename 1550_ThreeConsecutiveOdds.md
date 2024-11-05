# 🧠 Problem Title: Three Consecutive Odds

## Problem Statement
Given an integer array `arr`, return `true` if there are three consecutive odd numbers in the array, otherwise return `false`.

## Approach and Solution Explanation
The solution involves iterating through the array and checking each element along with the next two elements to see if they are all odd.

### Steps:
1. **Initialize Variables**: First, get the length of the array.
2. **Loop through the Array**: Iterate up to `n-2` to ensure there are three consecutive elements to check.
3. **Condition Check**: For each element at position `i`, check if `arr[i]`, `arr[i+1]`, and `arr[i+2]` are all odd. If they are, return `true` immediately.
4. **Return Result**: If no such sequence is found by the end of the loop, return `false`.

## Complexity Analysis
- **Time Complexity**: O(n), where n is the length of the array `arr`, as we only loop through the array once.
- **Space Complexity**: O(1), as we use a constant amount of additional space.

## Solution Code

```cpp
class Solution {
public:
    bool threeConsecutiveOdds(vector<int>& arr) {
        int n = arr.size();
        // Loop through the array up to the third-to-last element
        for(int i = 0; i < n - 2; i++) {
            // Check if the current element and the next two elements are all odd
            if(arr[i] % 2 == 1 && arr[i + 1] % 2 == 1 && arr[i + 2] % 2 == 1) {
                return true;
            }
        }
        return false;
    }
};
```

## Edge Cases to Consider
- Arrays with fewer than three elements (always returns `false`).
- Arrays where all elements are even or contain no sequence of three consecutive odd numbers.
---
