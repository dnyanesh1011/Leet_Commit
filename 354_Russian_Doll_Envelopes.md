# 🪆 Russian Doll Envelopes

## Problem Statement

You are given a 2D array of integers `envelopes` where `envelopes[i] = [wi, hi]` represents the width and height of an envelope. 

One envelope can fit into another if and only if both the width and height of one envelope are **greater than** the other envelope's width and height.

Return the maximum number of envelopes you can Russian doll (i.e., put one inside the other).

### Constraints:
- You cannot rotate an envelope.
- The dimensions of envelopes are positive integers.

---

## Examples

### Example 1:
**Input:**  
```cpp
envelopes = [[5,4],[6,4],[6,7],[2,3]]
```
**Output:**  
```cpp
3
```
**Explanation:**  
The maximum number of envelopes you can Russian doll is 3:  
\[ [2,3] \rightarrow [5,4] \rightarrow [6,7] \]

---

### Example 2:
**Input:**  
```cpp
envelopes = [[1,1],[1,1],[1,1]]
```
**Output:**  
```cpp
1
```
**Explanation:**  
All envelopes have the same dimensions, so only one can be used.

---

## Approach and Solution Explanation

The problem can be reduced to finding the **Longest Increasing Subsequence (LIS)** in two dimensions.

### Steps:
1. **Sort Envelopes**:
   - Sort the envelopes by width in ascending order.
   - If two envelopes have the same width, sort them by height in **descending order**. This ensures that envelopes with the same width cannot nest inside each other.
   
2. **Extract Heights**:
   - After sorting, extract the heights of the envelopes.

3. **Find LIS on Heights**:
   - Use a dynamic programming approach with a binary search optimization to find the LIS of the heights array.
   - This will give the maximum number of envelopes that can be nested.

---

## Solution Code

```cpp
class Solution {
public:
    int maxEnvelopes(vector<vector<int>>& envelopes) {
        // Step 1: Sort envelopes
        sort(envelopes.begin(), envelopes.end(), [](const vector<int>& a, const vector<int>& b) {
            if (a[0] == b[0]) {
                return a[1] > b[1]; // Sort by height in descending order for same width
            }
            return a[0] < b[0]; // Sort by width in ascending order
        });

        // Step 2: Extract heights
        vector<int> heights;
        for (const auto& envelope : envelopes) {
            heights.push_back(envelope[1]);
        }

        // Step 3: Find LIS
        vector<int> lis;
        for (int height : heights) {
            auto it = lower_bound(lis.begin(), lis.end(), height);
            if (it == lis.end()) {
                lis.push_back(height);
            } else {
                *it = height;
            }
        }

        return lis.size();
    }
};
```

---

## Complexity Analysis

### Time Complexity:
1. Sorting: \(O(n \log n)\), where \(n\) is the number of envelopes.
2. Finding LIS: \(O(n \log n)\), using binary search for each height.

**Total Complexity**: \(O(n \log n)\).

### Space Complexity:
- \(O(n)\), for storing the LIS array.

---

## Examples Walkthrough

### Example 1:
**Input:**  
```cpp
envelopes = [[5,4],[6,4],[6,7],[2,3]]
```
**Sorted Envelopes:**  
```cpp
[[2,3], [5,4], [6,7], [6,4]]
```
**Heights Extracted:**  
```cpp
[3, 4, 7, 4]
```
**LIS on Heights:**  
- Start with an empty list.
- Add `3`.
- Add `4`.
- Add `7`.
- Replace the second `4`.

Result: LIS length is `3`.

**Output:**  
```cpp
3
```

### Example 2:
**Input:**  
```cpp
envelopes = [[1,1],[1,1],[1,1]]
```
**Sorted Envelopes:**  
```cpp
[[1,1], [1,1], [1,1]]
```
**Heights Extracted:**  
```cpp
[1, 1, 1]
```
**LIS on Heights:**  
- Start with an empty list.
- Add `1`.

Result: LIS length is `1`.

**Output:**  
```cpp
1
```

---

## Conclusion

This solution efficiently solves the Russian Doll Envelopes problem by reducing it to finding the Longest Increasing Subsequence in one dimension after sorting the envelopes. The combination of sorting and binary search ensures an optimal time complexity of \(O(n \log n)\).
