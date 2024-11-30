# Decode String 🔑

## Problem Description

Given an encoded string, return its decoded string.

The encoding rule is:  
`k[encoded_string]`, where the `encoded_string` inside the square brackets is repeated exactly `k` times.  
Note that `k` is guaranteed to be a positive integer.

You may assume:
- The input string is always valid (e.g., no unmatched brackets).
- Digits are only used for the repeat count `k` and not part of the `encoded_string`.
- The original data does not contain digits unrelated to encoding (e.g., inputs like `3a` or `2[4]` are invalid).

---

## Examples

### Example 1:
**Input**:
```plaintext
s = "3[a]2[bc]"
```
**Output**:
```plaintext
"aaabcbc"
```

**Explanation**:  
The substring `"a"` is repeated `3` times, and `"bc"` is repeated `2` times.

---

### Example 2:
**Input**:
```plaintext
s = "3[a2[c]]"
```
**Output**:
```plaintext
"accaccacc"
```

**Explanation**:  
The substring `"a2[c]"` is decoded as `"acc"`, which is repeated `3` times.

---

### Example 3:
**Input**:
```plaintext
s = "2[abc]3[cd]ef"
```
**Output**:
```plaintext
"abcabccdcdcdef"
```

**Explanation**:  
- `"abc"` is repeated `2` times: `"abcabc"`.
- `"cd"` is repeated `3` times: `"cdcdcd"`.
- Concatenate the results with `"ef"`.

---

## Approach

### Key Insights

1. **Stack-Based Parsing**:
   - Use a stack to handle nested and sequential encodings.
   - Push intermediate results onto the stack and process them as brackets are closed.

2. **Character Categorization**:
   - Parse the string character by character:
     - Digits (`k`): Build the repeat count.
     - `[`: Start a new encoded substring.
     - `]`: Decode the substring by popping from the stack.
     - Letters: Append directly to the current substring.

3. **Nested Decoding**:
   - Ensure the stack can handle nested structures (e.g., `3[a2[c]]`).

---

## Solution Steps

1. **Initialize Stacks**:
   - Use two stacks:
     - One for repeat counts (`k`).
     - One for strings (current substring being built).

2. **Iterate Through the String**:
   - When encountering a digit, build the repeat count.
   - When encountering `[`, push the current substring and count onto their respective stacks.
   - When encountering `]`, pop from the stacks and construct the decoded substring.

3. **Build the Result**:
   - Concatenate all parts of the string as they are processed.

---

## Complexity Analysis

### Time Complexity
- **Single Pass**: Each character in the string is processed exactly once.
- **Decoding Substrings**: Each decoding operation involves appending strings, which takes \(O(n)\) over the entire input.

**Overall Complexity**: \(O(n)\), where \(n\) is the length of the input string.

### Space Complexity
- **Stacks**: Both stacks store partial results. In the worst case, all characters could be stored.

**Overall Complexity**: \(O(n)\).

---

## Solution Code

```cpp
class Solution {
public:
    string decodeString(string s) {
        stack<int> counts; // Stack to store repeat counts
        stack<string> resultStack; // Stack to store partial results
        string current = ""; // Current substring being built
        int k = 0; // Current repeat count
        
        for (char c : s) {
            if (isdigit(c)) {
                k = k * 10 + (c - '0'); // Build the repeat count
            } else if (c == '[') {
                counts.push(k); // Push the repeat count onto the stack
                resultStack.push(current); // Push the current substring onto the stack
                k = 0; // Reset the repeat count
                current = ""; // Start a new substring
            } else if (c == ']') {
                int repeat = counts.top(); counts.pop(); // Get the repeat count
                string temp = current;
                current = resultStack.top(); resultStack.pop(); // Get the previous substring
                while (repeat--) {
                    current += temp; // Append the repeated substring
                }
            } else {
                current += c; // Append the character to the current substring
            }
        }
        
        return current; // Return the final decoded string
    }
};
```

---

## Example Walkthrough

### Input: `s = "3[a2[c]]"`

1. **Initial Input**: `"3[a2[c]]"`
2. **Processing**:
   - Parse `3` → Push count `3`.
   - Parse `[` → Push empty substring.
   - Parse `a` → Append to substring.
   - Parse `2` → Push count `2`.
   - Parse `[` → Push current substring.
   - Parse `c` → Append to substring.
   - Parse `]` → Decode `"cc"`.
   - Parse `]` → Decode `"accaccacc"`.
3. **Output**: `"accaccacc"`

---

## Edge Cases

1. **No Encoding**:
   - Input: `"abc"`
   - Output: `"abc"`

2. **Empty Input**:
   - Input: `""`
   - Output: `""`

3. **Nested Encoding**:
   - Input: `"2[3[a]b]"`
   - Output: `"aaabaaab"`

---
