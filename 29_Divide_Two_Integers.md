# Divide Two Integers ➗

## Problem Description

You are tasked with dividing two integers, `dividend` and `divisor`, **without using** the following operators:
- Multiplication (`*`)
- Division (`/`)
- Modulus (`%`)  

The result must **truncate toward zero** (i.e., remove the fractional part).  

### Constraints:
- The result must fit within the range of a **32-bit signed integer**: \([-2^{31}, 2^{31} - 1]\).  
- If the result exceeds this range, return the maximum or minimum bound accordingly.  

---

## Examples

### Example 1:  
**Input**:  
```plaintext
dividend = 10, divisor = 3
```  
**Output**:  
```plaintext
3
```  
**Explanation**:  
\(10 \div 3 = 3.33333\ldots\) truncated to 3.  

---

### Example 2:  
**Input**:  
```plaintext
dividend = 7, divisor = -3
```  
**Output**:  
```plaintext
-2
```  
**Explanation**:  
\(7 \div -3 = -2.33333\ldots\) truncated to -2.  

---

### Example 3:  
**Input**:  
```plaintext
dividend = -2147483648, divisor = -1
```  
**Output**:  
```plaintext
2147483647
```  
**Explanation**:  
Since the result exceeds the 32-bit signed integer range, return \(2^{31} - 1 = 2147483647\).  

---

## Approach and Solution Explanation

### Key Insights

1. **Binary Search / Bit Manipulation**:
   - Use subtraction and shifting to simulate division.
   - Repeatedly subtract powers of two of the divisor from the dividend, reducing the problem size exponentially.

2. **Sign Handling**:
   - Division results in a positive value if **dividend** and **divisor** have the same sign, otherwise negative.

3. **Edge Cases**:
   - Handle cases where the result exceeds the 32-bit signed integer range.
   - Handle division by 1 and -1 for efficiency.

---

### Algorithm Steps

1. **Handle Edge Cases**:
   - If \( \text{dividend} = -2^{31} \) and \( \text{divisor} = -1 \), return \(2^{31} - 1\).  

2. **Determine the Sign of the Result**:
   - Calculate `positive` as `true` if dividend and divisor have the same sign.

3. **Convert to Positive**:
   - Work with absolute values of dividend and divisor to simplify calculations.

4. **Bitwise Subtraction**:
   - Use left shifts (\(\ll\)) to find the largest multiple of the divisor that can be subtracted from the dividend.

5. **Accumulate the Quotient**:
   - Track how many times the divisor (or its shifted multiples) were subtracted.

6. **Apply the Sign**:
   - Adjust the result based on the `positive` flag.

7. **Return the Result**:
   - Clamp the result within the 32-bit signed integer range.

---

### Complexity Analysis

1. **Time Complexity**:  
   - \(O(\log(\text{dividend}))\): Subtraction and shifting reduce the dividend exponentially.  

2. **Space Complexity**:  
   - \(O(1)\): Constant space is used.  

---

## Solution Code

```cpp
class Solution {
public:
    int divide(int dividend, int divisor) {
        // Handle edge case for overflow
        if (dividend == INT_MIN && divisor == -1) return INT_MAX;

        // Determine the sign of the result
        bool positive = (dividend > 0) == (divisor > 0);

        // Work with absolute values to simplify calculations
        long long absDividend = abs((long long)dividend);
        long long absDivisor = abs((long long)divisor);

        // Initialize the quotient
        int quotient = 0;

        // Subtract powers of divisor from dividend
        while (absDividend >= absDivisor) {
            long long temp = absDivisor, multiple = 1;
            while (absDividend >= (temp << 1)) {
                temp <<= 1;
                multiple <<= 1;
            }
            absDividend -= temp;
            quotient += multiple;
        }

        // Apply the sign and return the result
        return positive ? quotient : -quotient;
    }
};
```

---

## Example Walkthrough

### Input: `dividend = 10, divisor = 3`

1. **Absolute Values**:  
   \( \text{absDividend} = 10, \text{absDivisor} = 3 \).  

2. **Subtract Multiples**:  
   - \(10 - 6 = 4\) (subtract \(3 \times 2\)).  
   - \(4 - 3 = 1\) (subtract \(3 \times 1\)).  

3. **Quotient**:  
   \(2 + 1 = 3\).  

4. **Sign**:  
   Both are positive. Return \(3\).  

---

## Edge Cases

1. **Division Overflow**:  
   - Input: `dividend = -2147483648, divisor = -1`.  
   - Output: \(2147483647\).  

2. **Divisor is ±1**:  
   - Input: `dividend = 123, divisor = 1`.  
   - Output: \(123\).  

3. **Zero Handling**:  
   - Input: `dividend = 0, divisor = 5`.  
   - Output: \(0\).  

---

## Key Notes

- Efficient bitwise subtraction replaces costly division operations.
- Edge case handling ensures correctness for overflow and zero divisor scenarios.
