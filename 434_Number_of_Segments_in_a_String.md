# 🔢 Count Segments in a String

## Problem Statement

Given a string `s`, return the **number of segments** in the string.  
A segment is defined as a contiguous sequence of **non-space characters**.

---

## Examples

### Example 1:
**Input**:  
`s = "Hello, my name is John"`  
**Output**:  
`5`  

**Explanation**:  
The five segments are: `["Hello,", "my", "name", "is", "John"]`.

---

### Example 2:
**Input**:  
`s = "Hello"`  
**Output**:  
`1`  

**Explanation**:  
The single segment is `["Hello"]`.

---

### Example 3:
**Input**:  
`s = "   "`  
**Output**:  
`0`  

**Explanation**:  
No non-space characters exist, so there are no segments.

---

## Approach

1. **Traverse the String**:
   - Iterate through each character of the string.

2. **Count New Segments**:
   - Start a new segment when encountering a non-space character after a space or the start of the string.

3. **Handle Continuous Segments**:
   - Track whether you're currently in a segment using a `bool inSegment` variable.

4. **Return the Total Count**:
   - Return the number of segments counted during traversal.

---

## Solution Code

```cpp
class Solution {
public:
    int countSegments(string s) {
        int count = 0;       // Count of segments
        bool inSegment = false; // Flag to track if inside a segment

        for (char c : s) {
            if (c != ' ') { // Non-space character
                if (!inSegment) { 
                    count++; // Start new segment
                    inSegment = true;
                }
            } else {
                inSegment = false; // End current segment
            }
        }

        return count; // Total number of segments
    }
};
```

---

## Complexity Analysis

### Time Complexity:
- \(O(n)\), where \(n\) is the length of the string `s`.  
  The string is traversed once.

### Space Complexity:
- \(O(1)\).  
  No additional data structures are used.

---

## Edge Cases to Consider

1. **Empty String**:
   - Input: `s = ""`  
   - Output: `0`  

2. **String with Only Spaces**:
   - Input: `s = "   "`  
   - Output: `0`  

3. **String with Multiple Spaces Between Words**:
   - Input: `s = "Hello   World"`  
   - Output: `2`  

4. **String with No Spaces**:
   - Input: `s = "HelloWorld"`  
   - Output: `1`  

---

This solution efficiently counts segments in the string with clear logic and minimal overhead. 🚀
