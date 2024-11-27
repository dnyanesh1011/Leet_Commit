# 🔍 Contains Nearby Almost Duplicate  

## Problem Statement  

You are given an integer array `nums` and two integers `indexDiff` and `valueDiff`. Your task is to determine if there exist two indices \(i\) and \(j\) such that:  

1. \(i \neq j\),  
2. \(|i - j| \leq \text{indexDiff}\), and  
3. \(|\text{nums}[i] - \text{nums}[j]| \leq \text{valueDiff}\).  

Return `true` if such a pair exists, otherwise return `false`.  

---

## Examples  

### Example 1  

**Input**:  
```plaintext  
nums = [1, 2, 3, 1], indexDiff = 3, valueDiff = 0  
```  
**Output**:  
```plaintext  
true  
```  
**Explanation**:  
Pair \((i, j) = (0, 3)\) satisfies all conditions.  

### Example 2  

**Input**:  
```plaintext  
nums = [1, 5, 9, 1, 5, 9], indexDiff = 2, valueDiff = 3  
```  
**Output**:  
```plaintext  
false  
```  
**Explanation**:  
No pair satisfies the conditions.  

---

## Approach and Explanation  

### Sliding Window with Sorted Set  

The key is to maintain a sliding window of size `indexDiff` and ensure values in the window differ by at most `valueDiff`.  

### Algorithm  

1. Use a `set` to store the elements in the current sliding window.  
2. For each element \(i\):  
   - Remove the element that is no longer in the window (if \(i > \text{indexDiff}\)).  
   - Use `set.lower_bound` to find the smallest element in the window greater than or equal to \(\text{nums}[i] - \text{valueDiff}\).  
   - Check if this element satisfies the conditions for \(i\) and \(j\).  
3. If no pair is found after processing all elements, return `false`.  

---

## Solution Code  

```cpp  
class Solution {  
public:  
    bool containsNearbyAlmostDuplicate(vector<int>& nums, int indexDiff, int valueDiff) {  
        if (indexDiff <= 0 || valueDiff < 0) {  
            return false;  
        }  

        set<long> window;  
        for (int i = 0; i < nums.size(); ++i) {  
            if (i > indexDiff) {  
                window.erase(nums[i - indexDiff - 1]);  
            }  

            auto pos = window.lower_bound(static_cast<long>(nums[i]) - valueDiff);  
            if (pos != window.end() && *pos <= static_cast<long>(nums[i]) + valueDiff) {  
                return true;  
            }  

            window.insert(nums[i]);  
        }  

        return false;  
    }  
};  
```  

---

## Complexity Analysis  

- **Time Complexity**: \(O(n \cdot \log(\text{indexDiff}))\)  
  - Inserting into and removing from the `set` takes \(O(\log(\text{indexDiff}))\).  
- **Space Complexity**: \(O(\text{indexDiff})\)  
  - The size of the `set` is bounded by `indexDiff`.  

---

## Edge Cases  

1. **Empty Array**:  
   Input: `nums = []`  
   Output: `false`  

2. **Small `indexDiff` or `valueDiff`**:  
   Input: `nums = [1, 2, 3], indexDiff = 1, valueDiff = 0`  
   Output: `false`  

3. **Negative Values**:  
   Input: `nums = [-1, -2, -3], indexDiff = 2, valueDiff = 1`  
   Output: `true`  

---

## Conclusion  

This solution leverages a sliding window and a sorted set to efficiently check the conditions in \(O(n \cdot \log(\text{indexDiff}))\) time complexity while maintaining the sliding window constraint.
