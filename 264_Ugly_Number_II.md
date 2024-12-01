# Ugly Number II 🌟

## Problem Description

An **ugly number** is a positive integer whose prime factors are limited to **2, 3, and 5**.  

Given an integer `n`, return the **nth ugly number** in the sequence.  

---

## Examples

### Example 1:  
**Input**:  
```plaintext
n = 10
```  
**Output**:  
```plaintext
12
```  
**Explanation**:  
The first 10 ugly numbers are:  
\[1, 2, 3, 4, 5, 6, 8, 9, 10, 12\].  

---

### Example 2:  
**Input**:  
```plaintext
n = 1
```  
**Output**:  
```plaintext
1
```  
**Explanation**:  
1 is considered an ugly number as it has no prime factors.  

---

## Approach and Solution Explanation

### Key Insights

1. **Generate in Order**:
   - Use a **dynamic programming** approach to generate the sequence of ugly numbers in ascending order.

2. **Track Multiples**:
   - Maintain three indices (or pointers) for multiples of **2, 3, and 5**.
   - These pointers ensure the next smallest multiple for each prime factor is efficiently computed.

3. **Avoid Duplicates**:
   - If multiple primes contribute the same value (e.g., both \(2 \times 6\) and \(3 \times 4\) give 12), advance all relevant pointers.

4. **Iterative Generation**:
   - Use a loop to generate the sequence until the nth ugly number is reached.

---

### Algorithm Steps

1. **Initialization**:
   - Create a list `dp` to store the first \(n\) ugly numbers.  
   - Initialize the first ugly number as 1 (`dp[0] = 1`).  

2. **Maintain Indices**:
   - Use three pointers `i2`, `i3`, and `i5` to track the current position of multiples for 2, 3, and 5.  
   - Start with `i2 = i3 = i5 = 0`.

3. **Compute Next Ugly Number**:
   - At each step, calculate the next ugly number as the **minimum** of:
     - \(dp[i2] \times 2\), \(dp[i3] \times 3\), and \(dp[i5] \times 5\).  

4. **Update Indices**:
   - Increment the corresponding pointer(s) if their multiple was chosen as the next ugly number.  

5. **Repeat Until n**:
   - Continue until all \(n\) ugly numbers are computed.

---

### Complexity Analysis

1. **Time Complexity**:  
   - \(O(n)\): Each iteration computes the next ugly number and updates the pointers.

2. **Space Complexity**:  
   - \(O(n)\): The `dp` array stores the sequence of ugly numbers.

---

## Solution Code

```cpp
class Solution {
public:
    int nthUglyNumber(int n) {
        vector<int> dp(n); // To store the first n ugly numbers
        dp[0] = 1;         // The first ugly number is 1

        int i2 = 0, i3 = 0, i5 = 0; // Pointers for multiples of 2, 3, and 5

        for (int i = 1; i < n; ++i) {
            int nextUgly = min({dp[i2] * 2, dp[i3] * 3, dp[i5] * 5}); // Next ugly number
            dp[i] = nextUgly;

            if (nextUgly == dp[i2] * 2) i2++; // Increment pointer for 2
            if (nextUgly == dp[i3] * 3) i3++; // Increment pointer for 3
            if (nextUgly == dp[i5] * 5) i5++; // Increment pointer for 5
        }

        return dp[n - 1]; // Return the nth ugly number
    }
};
```

---

## Example Walkthrough

### Input: `n = 10`

1. Initialize `dp = [1]`.  
2. Compute values iteratively:  
   - \(1 \times 2 = 2\), \(1 \times 3 = 3\), \(1 \times 5 = 5\).  
   - Smallest is 2. Update `dp = [1, 2]`.  

3. Update Pointers:  
   - \(2 \times 2 = 4\), \(1 \times 3 = 3\), \(1 \times 5 = 5\).  
   - Smallest is 3. Update `dp = [1, 2, 3]`.  

4. Continue Until \(n = 10\):  
   - Sequence: `[1, 2, 3, 4, 5, 6, 8, 9, 10, 12]`.  

**Output**: `12`.  

---

## Edge Cases

1. **Small Input**:  
   - Input: `n = 1`.  
   - Output: `1`.  

2. **Large Input**:  
   - Ensure the algorithm efficiently computes for \(n = 10000\).  

3. **Handling Multiples**:  
   - Avoid duplicate calculations (e.g., \(2 \times 6\) and \(3 \times 4\)).  

--- 

## Key Notes

- Dynamic programming avoids brute force checks of prime factors.
- Efficient pointer updates ensure \(O(n)\) complexity.
