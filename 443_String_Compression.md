# 🔢 String Compression  

## Problem Statement  

You are given a character array `chars`. The goal is to compress it using the following rules:  

1. For each group of consecutive repeating characters in `chars`:  
   - If the group's length is 1, append only the character to the compressed array.  
   - Otherwise, append the character followed by the group's length (as individual digits).  

2. Modify the `chars` array **in-place**, and return the new length of the compressed array.  

### Constraints  

- Use **constant extra space**.  
- Input groups with lengths ≥ 10 must split the digits into separate characters.  

---

## Examples  

### Example 1  

**Input**:  
```plaintext  
chars = ["a","a","b","b","c","c","c"]  
```  
**Output**:  
```plaintext  
Return 6. chars = ["a","2","b","2","c","3"]  
```  
**Explanation**:  
- Groups: "aa", "bb", "ccc"  
- Compressed: "a2b2c3"  

### Example 2  

**Input**:  
```plaintext  
chars = ["a"]  
```  
**Output**:  
```plaintext  
Return 1. chars = ["a"]  
```  
**Explanation**:  
- Single character remains unchanged.  

### Example 3  

**Input**:  
```plaintext  
chars = ["a","b","b","b","b","b","b","b","b","b","b","b","b"]  
```  
**Output**:  
```plaintext  
Return 4. chars = ["a","b","1","2"]  
```  
**Explanation**:  
- Groups: "a", "bbbbbbbbbbbb"  
- Compressed: "ab12"  

---

## Approach  

### Steps  

1. **Initialize Two Pointers**:  
   - Use a pointer `write` to track where to write in the array.  
   - Use `read` to traverse the array.  

2. **Iterate Through Groups**:  
   - Identify consecutive repeating characters.  
   - Write the character to `chars[write]`.  
   - If the group size > 1, split its count into digits and write them.  

3. **Return `write` as the new length**:  
   - `write` tracks the length of the compressed array.  

---

## Solution Code  

```cpp  
class Solution {  
public:  
    int compress(vector<char>& chars) {  
        int write = 0, read = 0;  

        while (read < chars.size()) {  
            char currentChar = chars[read];  
            int count = 0;  

            // Count the occurrences of the current character  
            while (read < chars.size() && chars[read] == currentChar) {  
                ++read;  
                ++count;  
            }  

            // Write the character  
            chars[write++] = currentChar;  

            // Write the count (if > 1)  
            if (count > 1) {  
                string countStr = to_string(count);  
                for (char c : countStr) {  
                    chars[write++] = c;  
                }  
            }  
        }  

        return write;  
    }  
};  
```  

---

## Complexity Analysis  

### Time Complexity  
- **O(n)**:  
  - Each character is processed once.  

### Space Complexity  
- **O(1)**:  
  - In-place compression with no extra data structures.  

---

## Edge Cases  

1. **Single Character**:  
   - Input: `chars = ["a"]`  
   - Output: `1`  

2. **All Unique Characters**:  
   - Input: `chars = ["a","b","c"]`  
   - Output: `3`  

3. **Very Long Group**:  
   - Input: `chars = ["a", ..., "a"] (size = 100)`  
   - Output: Compressed length: `4` (`"a100"`)  

---

## Explanation  

### Input: `chars = ["a","a","b","b","c","c","c"]`  

1. **Initial Setup**:  
   - `write = 0`, `read = 0`.  

2. **Process 'a'**:  
   - Count = 2.  
   - Write `chars[0] = 'a'`, then `chars[1] = '2'`.  
   - `write = 2`, `read = 2`.  

3. **Process 'b'**:  
   - Count = 2.  
   - Write `chars[2] = 'b'`, then `chars[3] = '2'`.  
   - `write = 4`, `read = 4`.  

4. **Process 'c'**:  
   - Count = 3.  
   - Write `chars[4] = 'c'`, then `chars[5] = '3'`.  
   - `write = 6`, `read = 7`.  

Final result: `chars = ["a","2","b","2","c","3"]`. Return `6`.
