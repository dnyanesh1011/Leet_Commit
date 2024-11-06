# 🧠 Problem Title: Two Sum

## Problem Statement
Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to the `target`. You may assume that each input would have exactly one solution and you may not use the same element twice.

### Example:
**Input:** 
```cpp
nums = [2, 7, 11, 15], target = 9
```

**Output:** 
```cpp
[0, 1]
```
**Explanation:** 
Because nums[0] + nums[1] == 9, we return [0, 1].

## Approach and Solution Explanation
The solution uses a brute-force approach to find two numbers in the array that sum up to the target. It iterates through each element and checks if there is a second number in the array that, when added to the first, equals the target.

### Steps:
1. **Outer Loop**: Loop through the array and pick the first number.
2. **Inner Loop**: For each number picked in the outer loop, iterate over the remaining elements to find the second number.
3. **Condition Check**: For each pair of numbers, check if their sum equals the target.
4. **Return Result**: If a valid pair is found, return the indices of these two numbers. If no valid pair is found, return an empty array.

## Complexity Analysis
- **Time Complexity**: O(n^2), where `n` is the number of elements in the array. We iterate over each element and, for each, check all remaining elements.
- **Space Complexity**: O(1), as we use only a constant amount of extra space.

## Solution Code

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        // Loop through the array to find two numbers that add up to the target
        for (int i = 0; i < nums.size(); i++) {
            for (int j = i + 1; j < nums.size(); j++) {
                // Check if the sum of nums[i] and nums[j] equals the target
                if (nums[j] == target - nums[i]) {
                    return {i, j};  // Return the indices of the two numbers
                }
            }
        }
        // Return an empty vector if no solution is found
        return {};
    }
};
```

## Edge Cases to Consider
- If the array has less than two elements, no valid pair can exist, and the function should return an empty array.
- The function assumes there is exactly one solution, so you don't have to handle the case of no solution being found.
- If there are multiple pairs that add up to the target, the function will return the first valid pair it encounters.

---
