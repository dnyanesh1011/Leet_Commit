# 3Sum Closest

## Problem Description

Given an integer array `nums` of length `n` and an integer `target`, find three integers in `nums` such that the sum is closest to `target`.  

Return the **sum of the three integers**.  

You may assume that each input would have **exactly one solution**.

---

## Examples

### Example 1:
**Input**:  
```plaintext
nums = [-1, 2, 1, -4], target = 1
```  

**Output**:  
```plaintext
2
```  

**Explanation**:  
The sum that is closest to the target is \(2\):  
\[
-1 + 2 + 1 = 2
\]

---

### Example 2:
**Input**:  
```plaintext
nums = [0, 0, 0], target = 1
```  

**Output**:  
```plaintext
0
```  

**Explanation**:  
The sum that is closest to the target is \(0\):  
\[
0 + 0 + 0 = 0
\]

---

## Approach

### Key Insights

1. **Sorting**:
   - Sorting simplifies finding combinations and allows for efficient traversal.

2. **Two-Pointer Technique**:
   - For each fixed element, use two pointers (`left` and `right`) to find the closest sum for the remaining two elements.

3. **Optimal Checking**:
   - Track the smallest difference between the current sum and the target during traversal.

---

## Solution Steps

1. **Sort the Array**:
   - Sorting ensures that smaller values are to the left, which aids in efficient traversal.

2. **Iterate Through the Array**:
   - For each index `i`, treat `nums[i]` as the first element of the triplet.

3. **Use Two Pointers**:
   - Set `left = i + 1` and `right = n - 1`.
   - Calculate the sum of the three numbers (`nums[i]`, `nums[left]`, `nums[right]`).
   - Adjust the pointers based on whether the sum is less than or greater than the target.

4. **Update Closest Sum**:
   - Keep track of the closest sum and the minimum difference encountered.

5. **Return the Closest Sum**:
   - Once all elements have been processed, return the sum closest to the target.

---

## Complexity Analysis

### Time Complexity
- **Sorting**: \(O(n \log n)\)  
- **Two-Pointer Traversal**: \(O(n^2)\) (since for each fixed `i`, two pointers traverse the rest of the array).  
**Overall**: \(O(n^2)\)

### Space Complexity
- **In-place Sorting**: \(O(1)\)  

---

## Solution Code

```cpp
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        // Step 1: Sort the array
        sort(nums.begin(), nums.end());
        
        int closestSum = INT_MAX;
        int minDiff = INT_MAX;
        int n = nums.size();

        // Step 2: Iterate through the array
        for (int i = 0; i < n - 2; ++i) {
            int left = i + 1, right = n - 1;

            // Step 3: Two-pointer approach
            while (left < right) {
                int currentSum = nums[i] + nums[left] + nums[right];
                int currentDiff = abs(currentSum - target);

                // Update closest sum
                if (currentDiff < minDiff) {
                    minDiff = currentDiff;
                    closestSum = currentSum;
                }

                // Adjust pointers
                if (currentSum < target) {
                    ++left;
                } else if (currentSum > target) {
                    --right;
                } else {
                    // Exact match found
                    return currentSum;
                }
            }
        }

        return closestSum;
    }
};
```

---

## Example Walkthrough

### Input: `nums = [-1, 2, 1, -4], target = 1`

1. **Sort the Array**:  
   Sorted `nums = [-4, -1, 1, 2]`

2. **Iteration**:  
   - Fix `nums[0] = -4`:
     - Left: `nums[1] = -1`, Right: `nums[3] = 2`
     - Sum = \(-4 + -1 + 2 = -3\), Difference = \(4\)
     - Move `left` to `nums[2] = 1`, Sum = \(-4 + 1 + 2 = -1\), Difference = \(2\)
   - Fix `nums[1] = -1`:
     - Left: `nums[2] = 1`, Right: `nums[3] = 2`
     - Sum = \(-1 + 1 + 2 = 2\), Difference = \(1\)

3. **Output Closest Sum**: \(2\)

**Output**: \(2\)  

---

## Edge Cases

1. **All Zeros**:
   - Input: `nums = [0, 0, 0], target = 1`  
   - Output: \(0\) (sum is exactly \(0\)).

2. **Negative Target**:
   - Input: `nums = [-8, -4, -3, -2, -1], target = -10`  
   - Solution handles negative targets and sums.

3. **Large Inputs**:
   - Ensure solution handles up to \(n = 5000\) efficiently with \(O(n^2)\) complexity.
