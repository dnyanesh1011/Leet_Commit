# 📝 Remove Invalid Parentheses

## Problem Statement

Given a string `s` containing parentheses and letters, the goal is to **remove the minimum number of invalid parentheses** to make the string valid. A valid string has:

1. Balanced parentheses (`(` and `)` match correctly).
2. The order of letters and parentheses preserved.

### Constraints:
- You may return the results in any order.
- Return a **list of unique valid strings**.

---

## Examples

### Example 1:
**Input**:  
`s = "()())()"`  
**Output**:  
`["(())()", "()()()"]`  

---

### Example 2:
**Input**:  
`s = "(a)())()"`  
**Output**:  
`["(a())()", "(a)()()"]`  

---

### Example 3:
**Input**:  
`s = ")("`  
**Output**:  
`[""]`  

---

## Approach and Solution Explanation

The problem is solved using **Breadth-First Search (BFS)** to explore all possible strings obtained by removing invalid parentheses. The idea is to systematically generate shorter strings, stopping as soon as valid strings are found.

### Steps:

1. **Start with the Input String**:
   - Add the input string `s` to a queue for processing.
   - Use a `visited` set to track strings already processed to avoid duplicates.

2. **Validate Strings**:
   - For each string in the queue, check if it is valid using the helper function `isValid()`.
   - If valid, add it to the result and skip generating new strings.

3. **Generate New Strings**:
   - If a string is not valid, generate all possible strings by removing one parenthesis at a time.
   - Add only new, unvisited strings to the queue for further processing.

4. **Terminate When Valid Strings Are Found**:
   - Stop generating new strings once valid strings have been found at the current BFS level. This ensures the minimum number of removals.

---

## Solution Code

```cpp
class Solution {
public:
    vector<string> removeInvalidParentheses(string s) {
        vector<string> result; // To store valid strings
        unordered_set<string> visited; // To track processed strings
        queue<string> q; // Queue for BFS
        bool foundValid = false; // Flag to indicate if a valid string is found

        q.push(s);
        visited.insert(s);

        while (!q.empty()) {
            string current = q.front();
            q.pop();

            // Check if the current string is valid
            if (isValid(current)) {
                result.push_back(current); // Add valid string to the result
                foundValid = true; // Mark that a valid string is found
            }

            // Skip generating new strings if a valid string is already found
            if (foundValid) continue;

            // Generate strings by removing one parenthesis at a time
            for (int i = 0; i < current.length(); ++i) {
                if (current[i] != '(' && current[i] != ')') continue; // Skip non-parenthesis characters

                string next = current.substr(0, i) + current.substr(i + 1); // Remove the i-th character

                if (!visited.count(next)) { // If not visited
                    visited.insert(next);
                    q.push(next);
                }
            }
        }

        return result;
    }

private:
    // Helper function to check if a string has balanced parentheses
    bool isValid(const string& str) {
        int count = 0; // Track open parentheses
        for (char ch : str) {
            if (ch == '(') count++; // Increment for '('
            else if (ch == ')') {
                if (count == 0) return false; // More ')' than '('
                count--; // Match ')'
            }
        }
        return count == 0; // Valid if all '(' are matched
    }
};
```

---

## Complexity Analysis

### Time Complexity:
- BFS explores all possible strings. The worst case is \(O(2^n)\), where \(n\) is the length of the string.
- Checking validity with `isValid()` takes \(O(n)\).
- Overall: \(O(2^n \cdot n)\).

### Space Complexity:
- The `queue` and `visited` set store up to \(O(2^n)\) strings in the worst case.

---

## Edge Cases to Consider

1. **Empty String**:
   - Input: `""`
   - Output: `[""]`

2. **No Parentheses**:
   - Input: `"abc"`
   - Output: `["abc"]`

3. **Already Valid String**:
   - Input: `"()"`, `"(a)"`
   - Output: Same as input.

4. **Unbalanced String**:
   - Input: `"(()"`
   - Output: `["()"]`.

This BFS approach ensures all valid strings with the minimum number of removals are returned.
