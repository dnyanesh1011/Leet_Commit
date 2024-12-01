# Reverse Integer 🔄

## Problem Description

Given a signed 32-bit integer `x`, return the integer obtained by reversing its digits. If reversing the integer causes it to exceed the signed 32-bit integer range `[-2³¹, 2³¹ - 1]`, return `0`.

Additionally, assume the environment does not allow the use of 64-bit integers.

---

## Examples

### Example 1:
**Input**:  
```plaintext
x = 123
```
**Output**:  
```plaintext
321
```

---

### Example 2:
**Input**:  
```plaintext
x = -123
```
**Output**:  
```plaintext
-321
```

---

### Example 3:
**Input**:  
```plaintext
x = 120
```
**Output**:  
```plaintext
21
```

---

### Example 4:
**Input**:  
```plaintext
x = 0
```
**Output**:  
```plaintext
0
```

---

## Approach and Solution Explanation

### Key Insights

1. **Digit Extraction**:
   - Use the modulus operator `%` to extract the last digit of the number.
   - Use integer division `/` to remove the last digit.

2. **Reconstruct the Reversed Number**:
   - Start with an initial `reversedNumber = 0`.
   - Continuously extract the last digit and append it to `reversedNumber` by multiplying the current value by `10` and adding the extracted digit.

3. **Check for Overflow**:
   - Before appending the next digit, ensure that the current `reversedNumber` will not exceed the 32-bit signed integer limits when multiplied by `10`.

---

## Algorithm

1. **Initialize Variables**:
   - `reversedNumber` to store the reversed digits.

2. **Loop Through Digits**:
   - Extract the last digit using `x % 10`.
   - Update `x` by performing integer division (`x / 10`).

3. **Check for Overflow**:
   - Before updating `reversedNumber`, ensure it is within bounds:
     - If `reversedNumber > INT_MAX / 10` or `reversedNumber == INT_MAX / 10` and the next digit exceeds `7` (for positive overflow).
     - If `reversedNumber < INT_MIN / 10` or `reversedNumber == INT_MIN / 10` and the next digit exceeds `-8` (for negative overflow).

4. **Return Result**:
   - If no overflow occurs, return `reversedNumber`.
   - Otherwise, return `0`.

---

## Complexity Analysis

### Time Complexity
- **\(O(\log_{10} n)\)**: The number of iterations corresponds to the number of digits in the integer.

### Space Complexity
- **\(O(1)\)**: Constant space is used, independent of the input size.

---

## Solution Code

```cpp
class Solution {
public:
    int reverse(int x) {
        int reversedNumber = 0;

        while (x != 0) {
            int digit = x % 10; // Extract the last digit
            x /= 10; // Remove the last digit
            
            // Check for overflow
            if (reversedNumber > INT_MAX / 10 || (reversedNumber == INT_MAX / 10 && digit > 7)) {
                return 0;
            }
            if (reversedNumber < INT_MIN / 10 || (reversedNumber == INT_MIN / 10 && digit < -8)) {
                return 0;
            }

            // Append the digit to the reversed number
            reversedNumber = reversedNumber * 10 + digit;
        }

        return reversedNumber;
    }
};
```

---

## Example Walkthrough

### Input: `x = 123`

1. **Extract Digits**:
   - Digit: `3`, Remaining: `12`, Reversed: `3`
   - Digit: `2`, Remaining: `1`, Reversed: `32`
   - Digit: `1`, Remaining: `0`, Reversed: `321`

2. **Output**: `321`

---

### Input: `x = -123`

1. **Extract Digits**:
   - Digit: `-3`, Remaining: `-12`, Reversed: `-3`
   - Digit: `-2`, Remaining: `-1`, Reversed: `-32`
   - Digit: `-1`, Remaining: `0`, Reversed: `-321`

2. **Output**: `-321`

---

### Input: `x = 120`

1. **Extract Digits**:
   - Digit: `0`, Remaining: `12`, Reversed: `0`
   - Digit: `2`, Remaining: `1`, Reversed: `2`
   - Digit: `1`, Remaining: `0`, Reversed: `21`

2. **Output**: `21`

---

## Edge Cases

1. **Single Digit Input**:
   - Input: `x = 5`
   - Output: `5`

2. **Negative Number**:
   - Input: `x = -9`
   - Output: `-9`

3. **Overflow Check**:
   - Input: `x = 1534236469`
   - Output: `0` (reversed exceeds `INT_MAX`).

4. **Zero Input**:
   - Input: `x = 0`
   - Output: `0`

---
