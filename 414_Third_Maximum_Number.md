# 🥉 Third Maximum Number

## Problem Statement

Given an integer array `nums`, return the **third distinct maximum number** in this array. If the third maximum does not exist, return the maximum number instead.

--- 

## Examples

### Example 1:
**Input**:  
`nums = [3,2,1]`  
**Output**:  
`1`  

**Explanation**:  
- The first distinct maximum is `3`.  
- The second distinct maximum is `2`.  
- The third distinct maximum is `1`.  

---

### Example 2:
**Input**:  
`nums = [1,2]`  
**Output**:  
`2`  

**Explanation**:  
- The first distinct maximum is `2`.  
- The second distinct maximum is `1`.  
- The third distinct maximum does not exist, so the maximum (`2`) is returned instead.  

---

### Example 3:
**Input**:  
`nums = [2,2,3,1]`  
**Output**:  
`1`  

**Explanation**:  
- The first distinct maximum is `3`.  
- The second distinct maximum is `2`.  
- The third distinct maximum is `1`.  

---

## Approach

1. **Use a Set to Track Top Three Numbers**:
   - A `set` is used to maintain a sorted collection of unique elements.
   - Iterate through the array and insert each element into the set.
   - If the size of the set exceeds three, remove the smallest element to ensure it only stores the top three distinct numbers.

2. **Return Results**:
   - If the set has fewer than three elements, return the largest element (`*rbegin()` of the set).
   - Otherwise, return the smallest element in the set, which is the third maximum (`*begin()` of the set after maintaining the top three elements).

---

## Solution Code

```cpp
class Solution {
public:
    int thirdMax(vector<int>& nums) {
        set<int> topThree; // To store the top three distinct numbers

        for (int num : nums) {
            topThree.insert(num); // Insert the current number
            // If size exceeds three, remove the smallest element
            if (topThree.size() > 3) {
                topThree.erase(topThree.begin());
            }
        }

        // If there are fewer than three distinct numbers, return the maximum
        if (topThree.size() < 3) {
            return *topThree.rbegin();
        }

        // Otherwise, return the third maximum (smallest in the topThree set)
        return *topThree.begin();
    }
};
```

---

## Complexity Analysis

### Time Complexity:
- **Inserting into Set**: \(O(\log 3) = O(1)\) per insertion (since the set size is limited to 3).
- **Total**: \(O(n)\), where \(n\) is the size of the input array.

### Space Complexity:
- **Set Storage**: \(O(3) = O(1)\), as the set stores at most 3 elements.

---

## Edge Cases to Consider

1. **Array with Fewer than Three Distinct Numbers**:
   - Input: `nums = [2,2]`
   - Output: `2`

2. **Array with Exactly Three Distinct Numbers**:
   - Input: `nums = [3,2,1]`
   - Output: `1`

3. **Array with Repeated Maximums**:
   - Input: `nums = [1,2,2,3]`
   - Output: `1`

---

This solution efficiently determines the third distinct maximum using a set, ensuring correctness and clarity. 🥇🥈🥉
