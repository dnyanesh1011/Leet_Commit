#  ➕ Sum of Subsequence Widths

## Problem Description

The **width** of a sequence is defined as the difference between the **maximum** and **minimum** elements in the sequence.  
Given an array of integers `nums`, calculate the **sum of the widths** of all **non-empty subsequences** of `nums`.  

Since the result may be very large, return the result **modulo \(10^9 + 7\)**.

---

## Constraints

- \(1 \leq \text{nums.length} \leq 10^5\)  
- \(1 \leq \text{nums}[i] \leq 10^9\)  

---

## Examples

### Example 1:
**Input**:  
```plaintext
nums = [2,1,3]
```  

**Output**:  
```plaintext
6
```  

**Explanation**:  
The subsequences are:  
\[ [1], [2], [3], [2,1], [2,3], [1,3], [2,1,3] \]  
The corresponding widths are:  
\[ 0, 0, 0, 1, 1, 2, 2 \]  
The sum of these widths is \(6\).

---

### Example 2:
**Input**:  
```plaintext
nums = [2]
```  

**Output**:  
```plaintext
0
```  

**Explanation**:  
The only subsequence is \([2]\), and its width is \(0\).

---

## Approach

### Key Observations
1. The number of subsequences in which an element is the **maximum** depends on its position in the sorted array.  
   - If the element is at index `i` (0-based index):  
     It is the maximum for \(2^i\) subsequences.
     
2. Similarly, the number of subsequences in which an element is the **minimum** depends on its position in the sorted array:  
   - If the element is at index `i`:  
     It is the minimum for \(2^{(n - i - 1)}\) subsequences.

3. The contribution of each element to the total sum can be calculated using the above counts:
   \[
   \text{Contribution} = \text{Element} \times (2^i - 2^{(n - i - 1)})
   \]

### Steps
1. **Sort the Input Array**:  
   Sorting simplifies identifying the maximum and minimum contributions of elements.

2. **Precompute Powers of 2**:  
   Use modular arithmetic to calculate \(2^i \mod (10^9 + 7)\) efficiently.

3. **Iterate Through the Array**:  
   For each element in the sorted array, calculate its contribution as both a maximum and a minimum.

4. **Sum Contributions Modulo \(10^9 + 7\)**:  
   Add all contributions, taking care of overflow using modulo.

---

## Solution Code

```cpp
class Solution {
public:
    int sumSubseqWidths(vector<int>& nums) {
        const int MOD = 1e9 + 7;
        int n = nums.size();

        // Sort the array
        sort(nums.begin(), nums.end());

        // Precompute powers of 2 modulo MOD
        vector<long long> pow2(n, 1);
        for (int i = 1; i < n; ++i) {
            pow2[i] = (pow2[i - 1] * 2) % MOD;
        }

        long long result = 0;

        // Calculate the contribution of each element
        for (int i = 0; i < n; ++i) {
            result += nums[i] * (pow2[i] - pow2[n - i - 1]);
            result %= MOD;
        }

        // Ensure non-negative result
        if (result < 0) result += MOD;

        return result;
    }
};
```

---

## Complexity Analysis

### Time Complexity
- **Sorting**: \(O(n \log n)\)  
- **Iteration**: \(O(n)\)  
- **Precomputation**: \(O(n)\)  
**Overall**: \(O(n \log n)\)

### Space Complexity
- **Extra Storage for Powers**: \(O(n)\)  
**Overall**: \(O(n)\)

---

## Edge Cases
1. **Empty or Single Element List**:  
   Input: `nums = []` or `nums = [x]`  
   Output: `0`  

2. **All Elements Equal**:  
   Input: `nums = [k, k, k]`  
   Output: `0` (as all subsequences have width \(0\)).  

3. **Large Array and Values**:  
   Ensure the solution handles \(n = 10^5\) and values up to \(10^9\) efficiently.  

---

## Example Walkthrough

### Input: `nums = [2,1,3]`  

1. **Sort**: \([1, 2, 3]\)  
2. **Precompute**:  
   \(2^i \mod (10^9 + 7) = [1, 2, 4]\)  
3. **Calculate Contributions**:  
   - \(1: (2^0 - 2^2) = 1 - 4 = -3\)  
   - \(2: (2^1 - 2^1) = 2 - 2 = 0\)  
   - \(3: (2^2 - 2^0) = 4 - 1 = 3\)  
4. **Sum**: \(-3 + 0 + 3 = 6\) (mod \(10^9 + 7\))  

**Output**: \(6\)
