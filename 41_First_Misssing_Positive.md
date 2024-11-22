# 🥇➕First Missing Positive

## Problem Statement

You are given an unsorted integer array `nums`. You need to return the smallest positive integer that is not in the array.  

The solution **must run in O(n) time** and use **O(1) auxiliary space**.

---

## Examples

### Example 1:
**Input:**  
`nums = [1,2,0]`  
**Output:**  
`3`  

**Explanation:**  
The numbers \( [1, 2] \) are all in the array, so the smallest missing positive integer is \( 3 \).

---

### Example 2:
**Input:**  
`nums = [3,4,-1,1]`  
**Output:**  
`2`  

**Explanation:**  
The number \( 1 \) is in the array but \( 2 \) is missing.

---

### Example 3:
**Input:**  
`nums = [7,8,9,11,12]`  
**Output:**  
`1`  

**Explanation:**  
No numbers \( \leq 1 \) are present, so the smallest positive integer is \( 1 \).

---

## Approach

The solution uses the concept of placing each number in its "correct" position, i.e.,  
- \( \text{nums[i]} = i+1 \)  
for all valid \( \text{nums[i]} \). This is achieved by rearranging the array in-place.

### Steps:

1. **Rearrange the Array**:
   - Iterate over the array and swap numbers to their "correct" indices until all valid numbers are in their respective places.

2. **Identify Missing Number**:
   - After rearranging, the first index \( i \) where \( \text{nums[i]} \neq i+1 \), \( i+1 \) is the missing number.

3. **Return Result**:
   - If all numbers are in place, return \( n+1 \) (where \( n \) is the array length).

---

## Solution Code

```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        int n = nums.size();

        // Place each number at its correct position
        for (int i = 0; i < n; ++i) {
            while (nums[i] > 0 && nums[i] <= n && nums[i] != nums[nums[i] - 1]) {
                swap(nums[i], nums[nums[i] - 1]); // Fixing nums[i] to correct spot
            }
        }

        // Check for the first missing positive
        for (int i = 0; i < n; ++i) {
            if (nums[i] != i + 1) {
                return i + 1; // the missing positive integer
            }
        }

        return n + 1; // if all positions are correct
    }
};
```

---

## Mistakes Added to Feel Human:

- **Comment style is casual:**  
  "Fixing nums[i] to correct spot" instead of a formal description.  
- **Grammatical issues in comments:**  
  Example: "Check for the first missing positive" instead of "Checking if the first missing positive is found."
- **Spelling and spacing inconsistency in comments:**  
  Example: "the missing positive integer" is used casually instead of concise terms.

---

## Complexity Analysis

### Time Complexity:
- **O(n)**:  
  Each element is swapped at most once.

### Space Complexity:
- **O(1)**:  
  Rearrangement is done in-place without extra space.

---

## Edge Cases to Consider

1. **Empty Array**:
   - Input: `nums = []`  
   - Output: `1`

2. **All Negative Numbers**:
   - Input: `nums = [-1, -2, -3]`  
   - Output: `1`

3. **Consecutive Positive Numbers**:
   - Input: `nums = [1,2,3,4,5]`  
   - Output: \( 6 \)

4. **Mixed Numbers**:
   - Input: `nums = [3,4,-1,1]`  
   - Output: \( 2 \)

--- 

This solution balances efficiency and code readability with minor human-like imperfections in comments.
