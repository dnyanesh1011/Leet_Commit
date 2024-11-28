# 🔢 Permutations  

## Problem Statement  

Given an array `nums` of distinct integers, return all the possible **permutations**. You can return the answer in any order.  

---

## Examples  

### Example 1  

**Input**:  
```plaintext  
nums = [1,2,3]  
```  
**Output**:  
```plaintext  
[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]  
```  

### Example 2  

**Input**:  
```plaintext  
nums = [0,1]  
```  
**Output**:  
```plaintext  
[[0,1],[1,0]]  
```  

### Example 3  

**Input**:  
```plaintext  
nums = [1]  
```  
**Output**:  
```plaintext  
[[1]]  
```  

---

## Approach  

### Backtracking  

1. **Key Idea**:  
   Generate all possible permutations by swapping elements during recursion.  

2. **Steps**:  
   - Use a backtracking function to generate permutations.  
   - At each step, swap the current element with others and proceed recursively.  
   - Backtrack by undoing the swap to explore other possibilities.  

3. **Edge Cases**:  
   - If the input array is empty, return an empty list.  
   - If the input array has one element, return the array as the only permutation.  

---

## Solution Code  

```cpp  
class Solution {  
public:  
    vector<vector<int>> permute(vector<int>& nums) {  
        vector<vector<int>> result;  
        backtrack(nums, 0, result);  
        return result;  
    }  

private:  
    void backtrack(vector<int>& nums, int start, vector<vector<int>>& result) {  
        if (start == nums.size()) {  
            result.push_back(nums);  
            return;  
        }  

        for (int i = start; i < nums.size(); ++i) {  
            swap(nums[start], nums[i]);  
            backtrack(nums, start + 1, result);  
            swap(nums[start], nums[i]); // Undo the swap  
        }  
    }  
};  
```  

---

## Complexity Analysis  

### Time Complexity  
- **O(N!)**: There are \(N!\) permutations for an array of size \(N\), and generating each takes \(O(N)\).  

### Space Complexity  
- **O(N)**: Space used by the recursion stack.  

---

## Edge Cases  

1. **Empty Input**:  
   Input: `nums = []`  
   Output: `[]`  

2. **Single Element**:  
   Input: `nums = [1]`  
   Output: `[[1]]`  

3. **Small Array**:  
   Input: `nums = [1,2]`  
   Output: `[[1,2],[2,1]]`  

---

## Conclusion  

This solution uses backtracking to efficiently generate permutations of the input array. It handles all edge cases and provides the answer in any order as required.
