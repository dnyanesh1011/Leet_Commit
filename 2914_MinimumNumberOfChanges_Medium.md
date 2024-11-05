# 🧠 Problem Title: Minimum Number of Changes to Make Binary String Beautiful

## Problem Statement
You are given a 0-indexed binary string `s` having an even length. A string is beautiful if it's possible to partition it into one or more substrings such that:

- Each substring has an even length.
- Each substring contains only 1's or only 0's.

You can change any character in `s` to 0 or 1. Return the minimum number of changes required to make the string `s` beautiful.

## Approach and Solution Explanation
The approach involves iterating through the string while counting consecutive characters. The key points of the logic are:

1. **Initialization**: Start with the first character and initialize counters for consecutive characters and the minimum changes required.
2. **Iterate through the string**: For each character, check if it matches the current character:
   - If it does, increment the consecutive count.
   - If it does not, determine if the count of the previous character was even or odd:
     - If even, start a new sequence.
     - If odd, increment the minimum changes count and reset the consecutive counter.
3. **Return the result**: Finally, return the total minimum changes required.

## Complexity Analysis
- **Time Complexity**: O(n), where n is the length of the string. We make a single pass through the string.
- **Space Complexity**: O(1), as we only use a few additional variables.

## Solution Code

```cpp
class Solution {
public:
    int minChanges(string s) {
        // Initialize with first character of string
        char currentChar = s[0];
        int consecutiveCount = 0;
        int minChangesRequired = 0;

        // Iterates through each character in the string
        for(int i = 0; i < s.length(); i++) {
            // If current character matches the previous sequence
            if(s[i] == currentChar) {
                consecutiveCount++;
                continue;
            }

            // If we have even count of character, start new sequence
            if(consecutiveCount % 2 == 0) {
                consecutiveCount = 1;
            }
            // If odd count, we need to change current character
            // to match previous sequence
            else {
                consecutiveCount = 0;
                minChangesRequired++;
            }

            // Update current character for next iteration
            currentChar = s[i];
        }

        return minChangesRequired;
    }
};
