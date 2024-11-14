# 🔢 Palindrome Number Check in C++

## Overview
This C++ program checks if a given integer is a palindrome without reversing the entire number. A palindromic integer reads the same forwards and backwards, such as `121` or `1331`. To perform this check, we use an efficient approach that only reverses half of the number and then compares the two halves.

## Features
- **Half-Reversal Check**: Instead of reversing the whole number, the program only reverses half, saving both time and space.
- **Edge Case Handling**: Handles negative numbers and numbers ending in zero (except zero itself) as non-palindromic by definition.
- **Efficiency**: With a time complexity of \(O(\log_{10}(n))\), this approach is more efficient than converting the number to a string or reversing it fully.

## Code

```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        // Edge case: negative numbers and multiples of 10 (except zero) can't be palindromic
        if (x < 0 || (x % 10 == 0 && x != 0)) {
            return false;
        }

        int reversedHalf = 0;
        // Reverse only half of the number
        while (x > reversedHalf) {
            reversedHalf = reversedHalf * 10 + x % 10;
            x /= 10;
        }

        // Check if the first half is equal to the reversed second half
        return x == reversedHalf || x == reversedHalf / 10;
    }
};
```

## Explanation of Key Functions

### `isPalindrome(int x)`
This function checks if the integer `x` is a palindrome by:
1. **Edge Cases**: Returning `false` immediately for negative numbers and multiples of 10 (except zero).
2. **Reversing Half the Number**: Reverses digits from the end until the original number `x` becomes less than or equal to `reversedHalf`.
3. **Comparison**: Returns `true` if `x` is equal to `reversedHalf` (even-length numbers) or `reversedHalf / 10` (odd-length numbers, ignoring the middle digit).

## Example Usage

```cpp
#include <iostream>
using namespace std;

int main() {
    Solution solution;
    int num = 121;
    cout << boolalpha << solution.isPalindrome(num); // Output: true
    return 0;
}
```

## Complexity Analysis

- **Time Complexity**: \(O(\log_{10}(n))\), since the number of digits is reduced by half with each iteration.
- **Space Complexity**: \(O(1)\), as only a few integer variables are used for the comparison.

## Edge Cases Considered
- **Negative Numbers**: Always returns `false` since they cannot be palindromic.
- **Numbers Ending in Zero**: Any number ending in zero, except zero itself, is not a palindrome.
- **Single Digit Numbers**: All single-digit numbers are palindromic and return `true`.
- **Odd vs Even Digits**: Works for both by dividing the reversed number appropriately in the final comparison.

## Summary
This program provides an optimized solution to check if an integer is a palindrome by reversing only half of the digits. By focusing on efficiency and handling common edge cases, it offers a clear and performant approach to the palindrome number problem.
