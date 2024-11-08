# 🔄➡️0️⃣ Move Zeroes to End

## Problem Statement
Given an array `nums`, move all `0` elements to the end of the array while retaining the order of non-zero elements. The array should be modified in place with minimum extra space.

### Example
**Input**:
```cpp
nums = [0, 1, 0, 3, 12]
```

**Output**:
```cpp
[1, 3, 12, 0, 0]
```

**Explanation**: The order of non-zero elements `[1, 3, 12]` remains the same, and all `0`s are moved to the end.

## Approach and Solution Explanation

This solution uses two main passes through the array:
1. **Count Zeros**: First, count the total number of zeros in `nums`.
2. **Build Result with Non-Zeros**: Iterate through `nums` to add only non-zero elements to a new array (`ans`), followed by appending the counted number of zeros to the end of this new array. Finally, the results in `ans` are copied back to `nums`.

### Steps
1. **Zero Counting**: Use a loop to count how many `0`s are in `nums`.
2. **Build Non-Zero Array**: Create a new array `ans` and add all non-zero elements to it in their original order.
3. **Append Zeros**: Using the zero count from step 1, append the appropriate number of `0`s to `ans`.
4. **Copy to Original Array**: Copy the elements from `ans` back to `nums` to reflect the modified arrangement.

### Complexity Analysis
- **Time Complexity**: \(O(n)\), where \(n\) is the size of `nums`, because we pass through `nums` twice.
- **Space Complexity**: \(O(n)\), since we use a separate array `ans` to store the results.

## Solution Code

```cpp
class Solution
{
public:
    void moveZeroes(vector<int> &nums)
    {
        int n = nums.size();

        // Count the zeros
        int numZeroes = 0;
        for (int i = 0; i < n; i++)
        {
            numZeroes += (nums[i] == 0);
        }

        // Make all non-zero elements retain their original order
        vector<int> ans;
        for (int i = 0; i < n; i++)
        {
            if (nums[i] != 0)
            {
                ans.push_back(nums[i]);
            }
        }

        // Move all zeroes to the end
        while (numZeroes--)
        {
            ans.push_back(0);
        }

        // Copy result back to original array
        for (int i = 0; i < n; i++)
        {
            nums[i] = ans[i];
        }
    }
};
```

## Edge Cases to Consider
- **No Zeros**: If there are no zeros in `nums`, the array should remain unchanged.
- **All Zeros**: If `nums` contains only `0`s, all elements should remain in their positions as zeros.
- **Mixed Zeros and Non-Zeros**: Ensure the solution handles cases where zeros are scattered throughout.
- **Single Element Array**: Both `[0]` and `[non-zero]` cases should work correctly.
