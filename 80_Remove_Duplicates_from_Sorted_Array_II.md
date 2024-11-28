# 🗑️ Remove Duplicates from Sorted Array II  

## Problem Statement  

Given an integer array `nums` sorted in non-decreasing order, remove duplicates **in-place** such that each unique element appears at most **twice**.  

- The relative order of the elements must remain the same.  
- Modify the array **in-place** with \(O(1)\) extra memory.  
- Return the number \(k\), which is the number of valid elements in the array.  

---

## Examples  

### Example 1  

**Input**:  
```plaintext  
nums = [1,1,1,2,2,3]  
```  
**Output**:  
```plaintext  
5, nums = [1,1,2,2,3,_]  
```  

### Example 2  

**Input**:  
```plaintext  
nums = [0,0,1,1,1,1,2,3,3]  
```  
**Output**:  
```plaintext  
7, nums = [0,0,1,1,2,3,3,_,_]  
```  

---

## Approach  

1. **Two Pointers Technique**:  
   - Use a slow pointer to track the position for writing valid elements.  
   - Use a fast pointer to iterate through the array.  

2. **Logic**:  
   - Allow each unique element to appear **at most twice**.  
   - Check the element at `nums[fast]` and decide if it should be written at `nums[slow]` based on the value of the previous two elements in the valid range.  

3. **Edge Cases**:  
   - Empty array: Return `0`.  
   - Single element array: Return `1`.  

---

## Solution Code  

```cpp  
class Solution {  
public:  
    int removeDuplicates(vector<int>& nums) {  
        int n = nums.size();  
        if (n <= 2) return n;  

        int slow = 2;  // Start slow pointer at index 2  
        for (int fast = 2; fast < n; ++fast) {  
            if (nums[fast] != nums[slow - 2]) {  
                nums[slow] = nums[fast];  
                ++slow;  
            }  
        }  

        return slow;  
    }  
};  
```  

---

## Complexity Analysis  

### Time Complexity  
- **O(n)**: Iterate through the array once.  

### Space Complexity  
- **O(1)**: No extra memory used apart from variables.  

---

## Edge Cases  

1. **Empty Array**:  
   Input: `nums = []`  
   Output: `0`  

2. **Single Element Array**:  
   Input: `nums = [1]`  
   Output: `1`  

3. **All Elements Unique**:  
   Input: `nums = [1,2,3,4,5]`  
   Output: `5`  

4. **All Elements Same**:  
   Input: `nums = [1,1,1,1,1]`  
   Output: `2`  

---

## Explanation of Code  

1. Initialize `slow = 2`.  
2. Iterate through `nums` starting from index 2 (`fast = 2`).  
3. If `nums[fast]` is not equal to `nums[slow - 2]`, update `nums[slow]` and increment `slow`.  
4. After the loop, `slow` will be the count of valid elements.  

---

## Conclusion  

This solution modifies the array in-place while ensuring \(O(1)\) space complexity and maintaining the relative order of elements. It efficiently handles edge cases and adheres to the problem constraints.
