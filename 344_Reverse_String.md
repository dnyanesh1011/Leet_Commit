# 🔄 Reverse String using Recursion in C++

## Overview
This C++ program demonstrates how to reverse a string (represented as a `vector` of characters) using a recursive approach. Instead of using loops, we implement a helper function that reverses the string by swapping characters at the start and end indices and recursively narrowing the range.

## Features
- **Recursive Approach**: The `reverseStringHelper` function performs the reversal by swapping elements from the outside towards the center.
- **Efficient and Clean**: The recursive solution eliminates the need for iterative loops, leading to a clean and concise implementation.
- **Base and Recursive Cases**: The base case stops recursion when the start index meets or exceeds the end index, ensuring that all characters are reversed in-place.

## Code

```cpp
#include <vector>
using namespace std;

class Solution {
public:
    // Recursive helper function to reverse the string
    void reverseStringHelper(vector<char>& s, int i, int j) {
        // Base case: stop if start index meets or exceeds end index
        if (i >= j) return;

        // Swap characters at index i and j
        char temp = s[i];
        s[i] = s[j];
        s[j] = temp;

        // Recursive call with updated indices
        reverseStringHelper(s, i + 1, j - 1);
    }

    void reverseString(vector<char>& s) {
        reverseStringHelper(s, 0, s.size() - 1);
    }
};
```

## Explanation of Key Functions

### `reverseString(vector<char>& s)`
This function initializes the recursive reversal by calling `reverseStringHelper` with the full range of indices in the vector.

### `reverseStringHelper(vector<char>& s, int i, int j)`
This helper function reverses the string by:
1. **Base Case**: Stopping the recursion when the start index `i` is greater than or equal to the end index `j`.
2. **Swap Operation**: Swapping characters at indices `i` and `j`.
3. **Recursive Call**: Calling itself with `i+1` and `j-1` to continue swapping characters moving inward.

## Example Usage

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    Solution solution;
    vector<char> s = {'h', 'e', 'l', 'l', 'o'};
    solution.reverseString(s);

    for (char c : s) {
        cout << c; // Output will be "olleh"
    }
    return 0;
}
```

## Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the number of characters in the string. Each character is involved in a single swap operation.
- **Space Complexity**: \(O(n)\) in the worst case due to recursive function calls stacking up on the call stack.

## Edge Cases Considered
- **Empty Vector**: An empty input vector will result in no swaps and return immediately.
- **Single Character**: A single-character vector will not perform any swaps, as the base case is met immediately.
- **Even and Odd Lengths**: Works correctly for both even-length (all characters swapped) and odd-length vectors (middle character remains unchanged).

## Summary
This program provides a recursive solution for reversing a string without the use of iterative loops. By leveraging the recursive `reverseStringHelper` function, the code achieves a clean, in-place reversal of the string's characters.
