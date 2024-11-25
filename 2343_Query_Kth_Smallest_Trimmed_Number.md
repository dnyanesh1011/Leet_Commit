#  🔹🔹Smallest Trimmed Numbers

## Problem Statement

Given an array of strings `nums` where each string is composed of digits and has the same length, and a 2D array `queries`, the goal is to:

1. **Trim** each number in `nums` to its last `trim` digits as specified in each query.
2. **Sort** the trimmed numbers lexicographically. If two trimmed numbers are equal, the one with the smaller original index comes first.
3. Find the index of the `k`-th smallest trimmed number for each query.
4. Reset `nums` to its original state before processing the next query.

The task is to return an array of indices corresponding to the `k`-th smallest trimmed number for each query.

---

## Example

### Example 1:
**Input**:
```cpp
nums = ["102", "473", "251", "814"]
queries = [[1, 1], [2, 3], [4, 2], [1, 2]]
```

**Output**:
```cpp
[2, 2, 1, 0]
```

**Explanation**:
1. Trim to last 1 digit: `["2", "3", "1", "4"]`. The smallest is `1` at index `2`.
2. Trim to last 3 digits: `["102", "473", "251", "814"]`. The 2nd smallest is `251` at index `2`.
3. Trim to last 2 digits: `["02", "73", "51", "14"]`. The 4th smallest is `73` at index `1`.
4. Trim to last 2 digits: `["02", "73", "51", "14"]`. The smallest is `02` at index `0`.

---

## Approach

### Key Steps:
1. **Extract Trimmed Numbers**: For each query, take the last `trim` digits of each number in `nums` and store them with their original indices.
2. **Sort the Trimmed Numbers**: Sort the trimmed numbers lexicographically. If two trimmed numbers are equal, sort by the original index.
3. **Find the k-th Smallest Number**: Use the sorted list to find the `k`-th smallest trimmed number.
4. **Repeat for Each Query**: Process each query independently.

### Algorithm:
1. Loop through each query in `queries`:
   - Extract the last `trim` digits of each number in `nums`.
   - Store the trimmed numbers along with their original indices.
   - Sort the trimmed numbers lexicographically.
   - Select the `k`-th smallest trimmed number's original index.
2. Append the result for each query to a result vector.
3. Return the result vector.

---

## Complexity Analysis

- **Time Complexity**:
  - For each query:
    - Trimming numbers: \(O(n \cdot \text{trim})\), where \(n\) is the size of `nums` and `trim` is the number of digits to extract.
    - Sorting: \(O(n \log n)\).
  - For \(q\) queries, the total complexity is \(O(q \cdot n \cdot (\text{trim} + \log n))\).

- **Space Complexity**:
  - Storing the trimmed numbers: \(O(n)\).
  - Total: \(O(n)\) per query.

---

## Implementation

### C++ Code:
```cpp
#include <vector>
#include <string>
#include <algorithm>
using namespace std;

class Solution {
public:
    vector<int> smallestTrimmedNumbers(vector<string>& nums, vector<vector<int>>& queries) {
        vector<int> result;
        
        for (auto& query : queries) {
            int k = query[0];
            int trim = query[1];
            
            // Vector to store trimmed numbers with their original indices
            vector<pair<string, int>> trimmed;
            
            for (int i = 0; i < nums.size(); ++i) {
                // Take the rightmost `trim` digits of nums[i]
                string trimmed_num = nums[i].substr(nums[i].size() - trim);
                trimmed.push_back({trimmed_num, i});
            }
            
            // Sort based on trimmed value
            sort(trimmed.begin(), trimmed.end(), [](const pair<string, int>& a, const pair<string, int>& b) {
                if (a.first == b.first)
                    return a.second < b.second; // Compare indices
                return a.first < b.first; // Compare trimmed values
            });
            
            result.push_back(trimmed[k - 1].second);
        }
        
        return result;
    }
};
```

---

## Example Walkthrough

### Input:
```cpp
nums = ["24", "37", "96", "04"]
queries = [[2, 1], [2, 2]]
```

### Steps:
1. **First Query ([2, 1])**:
   - Trim to last 1 digit: `["4", "7", "6", "4"]`.
   - Sorted: `["4", "4", "6", "7"]` with indices `[0, 3, 2, 1]`.
   - 2nd smallest: Index `3`.

2. **Second Query ([2, 2])**:
   - Trim to last 2 digits: `["24", "37", "96", "04"]`.
   - Sorted: `["04", "24", "37", "96"]` with indices `[3, 0, 1, 2]`.
   - 2nd smallest: Index `0`.

### Output:
```cpp
[3, 0]
```

---

## Conclusion

This implementation efficiently handles the problem of finding the `k`-th smallest trimmed number for multiple queries using sorting and substring operations. By leveraging sorting and lexicographical comparison, the algorithm ensures correctness and avoids duplicates in the results.
