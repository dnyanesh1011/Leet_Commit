# Permutation Sequence 🔢

## Problem Description

Given a set of numbers \([1, 2, 3, \dots, n]\), which contains a total of \(n!\) unique permutations, determine the \(k\)-th permutation sequence when all permutations are arranged in lexicographic order.

---

## Examples

### Example 1:
**Input**:  
```plaintext
n = 3, k = 3
```
**Output**:  
```plaintext
"213"
```
**Explanation**:  
The permutations of `[1, 2, 3]` in order are:
1. `"123"`
2. `"132"`
3. `"213"`
4. `"231"`
5. `"312"`
6. `"321"`
The \(3\)-rd permutation is `"213"`.

---

### Example 2:
**Input**:  
```plaintext
n = 4, k = 9
```
**Output**:  
```plaintext
"2314"
```
**Explanation**:  
The \(9\)-th permutation of `[1, 2, 3, 4]` is `"2314"`.

---

### Example 3:
**Input**:  
```plaintext
n = 3, k = 1
```
**Output**:  
```plaintext
"123"
```
**Explanation**:  
The \(1\)-st permutation of `[1, 2, 3]` is `"123"`.

---

## Approach and Solution Explanation

### Key Insights

1. **Factorial Division**:
   - The permutations can be divided into \(n\) groups of \((n-1)!\) permutations each. The position of \(k\) determines which group the \(k\)-th permutation belongs to.

2. **Lexicographic Ordering**:
   - Use the group index to select the corresponding number for the current position, then recursively process the remaining digits.

3. **Adjust Indices**:
   - Since \(k\) is 1-based, subtract \(1\) from \(k\) to make it 0-based for easier calculations.

---

### Algorithm

1. **Precompute Factorials**:
   - Calculate the factorial values from \(1\) to \(n\) to determine group sizes.

2. **Iteratively Select Digits**:
   - Use integer division and modulo operations to determine the index of the next number to be added to the permutation.

3. **Remove Selected Digits**:
   - Maintain a list of available digits and remove digits as they are used.

---

## Complexity Analysis

### Time Complexity
- **\(O(n^2)\)**:  
  - \(O(n)\) for factorial precomputation.
  - \(O(n)\) iterations for constructing the sequence, with \(O(n)\) for removing elements from the list.

### Space Complexity
- **\(O(n)\)**:  
  - Space for the factorial array and the list of digits.

---

## Solution Code

```cpp
class Solution {
public:
    string getPermutation(int n, int k) {
        vector<int> factorial(n, 1);
        vector<int> numbers;
        string result = "";

        // Precompute factorials and initialize the list of numbers
        for (int i = 1; i < n; ++i) {
            factorial[i] = factorial[i - 1] * i;
        }
        for (int i = 1; i <= n; ++i) {
            numbers.push_back(i);
        }

        // Adjust k to be 0-based
        --k;

        // Build the k-th permutation
        for (int i = n; i > 0; --i) {
            int idx = k / factorial[i - 1]; // Determine the index of the current digit
            result += to_string(numbers[idx]); // Append the digit to the result
            numbers.erase(numbers.begin() + idx); // Remove the used digit
            k %= factorial[i - 1]; // Update k for the next position
        }

        return result;
    }
};
```

---

## Example Walkthrough

### Input: `n = 3, k = 3`

1. **Precompute Factorials**:
   - Factorials: `[1, 1, 2]` (for \(1!, 2!, 3!\)).

2. **Available Digits**:
   - Initial: `[1, 2, 3]`.

3. **Determine Digits**:
   - \(k = 3 - 1 = 2\) (convert to 0-based).
   - First digit: \(2 / 2 = 1\), so pick `2`.  
     Updated digits: `[1, 3]`, \(k = 2 \% 2 = 0\).
   - Second digit: \(0 / 1 = 0\), so pick `1`.  
     Updated digits: `[3]`, \(k = 0 \% 1 = 0\).
   - Third digit: \(0 / 1 = 0\), so pick `3`.

4. **Output**: `"213"`

---

## Edge Cases

1. **Minimum Values**:
   - Input: `n = 1, k = 1`
   - Output: `"1"`

2. **First Permutation**:
   - Input: `n = 4, k = 1`
   - Output: `"1234"`

3. **Last Permutation**:
   - Input: `n = 3, k = 6`  
     (Last permutation for \(n = 3\)).
   - Output: `"321"`

---
