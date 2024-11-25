# 💬Text Justification

## Problem Statement

Given an array of words and a maximum width `maxWidth`, format the text such that each line has exactly `maxWidth` characters and is fully (left and right) justified.

- **Left and Right Justification**: Distribute spaces between words evenly. If spaces do not divide evenly, the leftmost slots get extra spaces.
- **Last Line**: The last line should be left-justified, with no extra spaces between words.
- Words will always have non-space characters, and the result must pad spaces as necessary to fit `maxWidth`.

---

## Examples

### Example 1:
**Input**:
```cpp
words = ["This", "is", "an", "example", "of", "text", "justification."], maxWidth = 16
```
**Output**:
```cpp
[
   "This    is    an",
   "example  of text",
   "justification.  "
]
```

---

### Example 2:
**Input**:
```cpp
words = ["What", "must", "be", "acknowledgment", "shall", "be"], maxWidth = 16
```
**Output**:
```cpp
[
   "What   must   be",
   "acknowledgment  ",
   "shall be        "
]
```

---

## Approach

### Steps to Solve the Problem:
1. **Group Words for Each Line**:
   - Start with the first word and group as many words as possible while ensuring their total length (including spaces) does not exceed `maxWidth`.

2. **Handle Different Types of Lines**:
   - **Fully Justified Lines**:
     - For lines that are not the last line and contain more than one word:
       - Distribute spaces between words as evenly as possible.
       - Extra spaces are added to the leftmost slots.
   - **Last Line or Single-Word Lines**:
     - These are left-justified.
     - All extra spaces are added to the right.

3. **Construct Each Line**:
   - Use `string` operations to build the justified line and append it to the result.

4. **Continue Until All Words are Processed**.

---

## Complexity Analysis

- **Time Complexity**:
  - Iterating through all words takes \(O(n)\), where \(n\) is the total number of words.
  - Building each line involves string operations proportional to the line width, so the complexity is \(O(k \cdot \text{maxWidth})\), where \(k\) is the number of lines.
  - Total: \(O(n + k \cdot \text{maxWidth})\).

- **Space Complexity**:
  - The result vector stores all lines, with a maximum size of \(O(k \cdot \text{maxWidth})\).

---

## Implementation

### C++ Code:
```cpp
#include <vector>
#include <string>
using namespace std;

class Solution {
public:
    vector<string> fullJustify(vector<string>& words, int maxWidth) {
        vector<string> result;
        int n = words.size();
        int i = 0;

        while (i < n) {
            int lineLength = words[i].length();
            int j = i + 1;

            // Group words that fit in the current line
            while (j < n && lineLength + words[j].length() + (j - i) <= maxWidth) {
                lineLength += words[j].length();
                ++j;
            }

            string line;
            int numWords = j - i;
            int totalSpaces = maxWidth - lineLength;

            if (j == n || numWords == 1) {
                // Last line or single word: left-justify
                for (int k = i; k < j; ++k) {
                    line += words[k];
                    if (k < j - 1) line += " ";
                }
                line += string(maxWidth - line.length(), ' ');
            } else {
                // Fully justified line
                int spacesPerSlot = totalSpaces / (numWords - 1);
                int extraSpaces = totalSpaces % (numWords - 1);

                for (int k = i; k < j; ++k) {
                    line += words[k];
                    if (k < j - 1) {
                        line += string(spacesPerSlot + (extraSpaces > 0 ? 1 : 0), ' ');
                        if (extraSpaces > 0) --extraSpaces;
                    }
                }
            }

            result.push_back(line);
            i = j;
        }

        return result;
    }
};
```

---

## Example Walkthrough

### Input:
```cpp
words = ["Science", "is", "what", "we", "understand", "well", "enough", "to", "explain", "to", "a", "computer.", "Art", "is", "everything", "else", "we", "do"]
maxWidth = 20
```

### Steps:
1. **Line 1**: 
   - Words: `["Science", "is", "what", "we"]`.
   - Total length: `20`.
   - Fully Justified: `"Science  is  what we"`.

2. **Line 2**:
   - Words: `["understand", "well"]`.
   - Total length: `20`.
   - Fully Justified: `"understand      well"`.

3. **Last Line**:
   - Words: `["do"]`.
   - Left-Justified: `"do                  "`.

### Output:
```cpp
[
   "Science  is  what we",
   "understand      well",
   "do                  "
]
```

---

## Conclusion

This implementation provides a clean and efficient solution to the text justification problem by grouping words, determining spacing, and handling edge cases like the last line or single-word lines effectively. The algorithm ensures each line adheres to the formatting requirements while maintaining the desired width.
