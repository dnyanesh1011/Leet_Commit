# 📝 Count and Say

## Problem Statement

The **count-and-say sequence** is a series of digit strings defined recursively:

1. **Base Case**: `countAndSay(1) = "1"`.
2. For \( n > 1 \), `countAndSay(n)` is the **run-length encoding** of the string `countAndSay(n-1)`.

Run-length encoding involves counting consecutive identical characters in a string and representing them as `<count><character>`. 

---

### Examples

#### Example 1:
**Input**:  
`n = 1`  
**Output**:  
`"1"`  
**Explanation**: This is the base case.

#### Example 2:
**Input**:  
`n = 4`  
**Output**:  
`"1211"`  
**Explanation**:  
- `countAndSay(1) = "1"`  
- `countAndSay(2) = "11"` (One `1`)  
- `countAndSay(3) = "21"` (Two `1`s)  
- `countAndSay(4) = "1211"` (One `2`, followed by One `1`)

---

## Approach and Solution Explanation

This problem can be solved recursively by generating the sequence for \( n \) based on \( n-1 \):

1. **Base Case**:
   - If \( n = 1 \), return `"1"`.
   
2. **Recursive Case**:
   - First, compute `countAndSay(n - 1)`.
   - Analyze the resulting string by grouping consecutive identical characters:
     - Count the number of occurrences of each character.
     - Append the count and the character to build the string for \( n \).

3. **Final Result**:
   - Return the string generated for \( n \).

---

## Solution Code

```cpp
class Solution {
public:
    string countAndSay(int n) {
        // Base case: The first sequence is always "1"
        if (n == 1) return "1";

        // Get the previous sequence by calling the function recursively
        string prev = countAndSay(n - 1);

        // To build the current sequence
        string result = "";
        int count = 1; // To count the occurrences of each digit

        // Loop through the previous sequence
        for (int i = 1; i < prev.size(); ++i) {
            if (prev[i] == prev[i - 1]) {
                // If the current character matches the previous, increment the count
                count++;
            } else {
                // If not, append the count and the previous character to the result
                result += to_string(count) + prev[i - 1];
                count = 1; // Reset count for the new character
            }
        }

        // Append the last group (leftover) to the result
        result += to_string(count) + prev.back();

        return result;
    }
};
```

---

## Complexity Analysis

### Time Complexity:
- For each \( n \), the algorithm processes the entire string for \( n-1 \).
- Since the string approximately doubles in size with each step, the complexity is **O(2^n)**.

### Space Complexity:
- The space used for recursion is proportional to \( n \), resulting in **O(n)**.

---

## Edge Cases to Consider

1. **Minimum Input**:
   - Input: `n = 1`
   - Output: `"1"`

2. **Larger Values**:
   - Ensure the function handles recursive depth for larger \( n \) (e.g., \( n = 15 \)).

---

## How the Algorithm Works

For \( n = 4 \), the sequence generation proceeds as follows:
1. \( countAndSay(1) = "1" \)
2. \( countAndSay(2) = "11" \) (One `1`)
3. \( countAndSay(3) = "21" \) (Two `1`s)
4. \( countAndSay(4) = "1211" \) (One `2`, One `1`)

This recursive approach ensures the correct sequence is generated efficiently.
