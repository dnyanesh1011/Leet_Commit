# 🤏Subsets II

## Problem Statement

Given an integer array `nums` that may contain duplicates, return all possible subsets (the power set). 

- The solution set **must not contain duplicate subsets**. 
- Return the subsets in **any order**.

---

## Examples

### Example 1:

**Input**:
```cpp
nums = [1, 2, 2]
```

**Output**:
```cpp
[[], [1], [1, 2], [1, 2, 2], [2], [2, 2]]
```

### Example 2:

**Input**:
```cpp
nums = [0]
```

**Output**:
```cpp
[[], [0]]
```

---

## Approach

### Key Idea
This problem is a variation of the "Subset" problem but includes duplicate elements. To handle duplicates, we sort the array and skip adding duplicate elements at the same recursion level.

### Steps:
1. **Sort the Array**:
   - Sorting ensures that duplicates are adjacent, making it easier to skip them.

2. **Backtracking**:
   - Start with an empty subset (`current`) and an empty result list (`result`).
   - For every element, either include it in the current subset or skip it.
   - Skip duplicate elements at the same recursion level to avoid duplicate subsets.
   - Recurse for the next element.

3. **Add Subsets**:
   - Each subset (`current`) is added to the result.

4. **Backtrack**:
   - After exploring all subsets including a specific element, remove it from `current` to explore subsets without it.

---

## Complexity Analysis

- **Time Complexity**:
  - Generating all subsets takes \(O(2^n)\), where \(n\) is the size of the array.
  - Sorting the array takes \(O(n \log n)\).
  - Total: \(O(2^n + n \log n)\).

- **Space Complexity**:
  - The recursion stack and the `current` subset require \(O(n)\) space.

---

## Implementation

### C++ Code:
```cpp
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        vector<vector<int>> result;
        vector<int> current;
        
        // Sort the array to handle duplicates
        sort(nums.begin(), nums.end());
        
        // Generate subsets
        backtrack(nums, 0, current, result);
        return result;
    }
    
private:
    void backtrack(vector<int>& nums, int start, vector<int>& current, vector<vector<int>>& result) {
        // Add the current subset to the result
        result.push_back(current);
        
        for (int i = start; i < nums.size(); ++i) {
            // Skip duplicates
            if (i > start && nums[i] == nums[i - 1]) continue;
            
            // Include the current element
            current.push_back(nums[i]);
            
            // Recur for the next elements
            backtrack(nums, i + 1, current, result);
            
            // Remove the current element (backtrack)
            current.pop_back();
        }
    }
};
```

---

## Example Walkthrough

### Input:
```cpp
nums = [1, 2, 2]
```

### Steps:
1. **Sort**: `nums = [1, 2, 2]`.
2. Start with an empty subset: `current = []`.
3. Add subsets recursively:
   - Include `1`: `current = [1]` → Add subsets `[1], [1, 2], [1, 2, 2]`.
   - Exclude `1`: Skip duplicates → Add subsets `[2], [2, 2]`.

### Output:
```cpp
[[], [1], [1, 2], [1, 2, 2], [2], [2, 2]]
```

---

## Conclusion

This solution ensures that duplicate subsets are avoided by sorting the input and skipping duplicates during recursion. It efficiently generates all unique subsets using a backtracking approach.
