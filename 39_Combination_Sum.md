# 🎯 Combination Sum

## Problem Overview

Given:
- An array of distinct integers `candidates`.
- A target integer `target`.

The task is to find all unique combinations of numbers from `candidates` that sum up to `target`.  
Numbers can be reused unlimited times in a combination, and combinations should be unique based on the frequency of elements.

---

## Examples

### Example 1
**Input**:  
```plaintext
candidates = [2,3,6,7], target = 7
```

**Output**:  
```plaintext
[[2, 2, 3], [7]]
```

**Explanation**:  
- Combination 1: \( 2 + 2 + 3 = 7 \)  
- Combination 2: \( 7 = 7 \)

---

### Example 2
**Input**:  
```plaintext
candidates = [2,3,5], target = 8
```

**Output**:  
```plaintext
[[2, 2, 2, 2], [2, 3, 3], [3, 5]]
```

**Explanation**:  
- Combination 1: \( 2 + 2 + 2 + 2 = 8 \)  
- Combination 2: \( 2 + 3 + 3 = 8 \)  
- Combination 3: \( 3 + 5 = 8 \)

---

### Example 3
**Input**:  
```plaintext
candidates = [2], target = 1
```

**Output**:  
```plaintext
[]
```

**Explanation**:  
No combination of numbers from `candidates` can sum to `target`.

---

## Approach and Solution Explanation

### Insight

The problem can be solved using **backtracking**, where:
- We recursively explore all possible combinations of the `candidates` array.
- At each step, we either:
  - Choose a number (reuse it because it can be used unlimited times).
  - Skip the number and move to the next candidate.

---

### Steps

1. **Sort the Input Array**:
   - Sorting helps to optimize the solution by allowing early termination of recursion for numbers exceeding `target`.

2. **Recursive Backtracking**:
   - Base Case:
     - If `target == 0`: Add the current combination to the result.
     - If `target < 0`: Terminate the recursion.
   - Recursive Step:
     - Iterate through the `candidates` starting from the current index.
     - Include the current number and recursively call for the remaining `target`.

3. **Avoid Duplicates**:
   - Ensure combinations are unique by tracking the start index of the iteration.

---

## Complexity Analysis

### Time Complexity:
- Worst-case: **O(2^T)**, where \(T\) is the `target`.
  - This is because each number can be chosen multiple times, leading to exponential combinations.

### Space Complexity:
- **O(T)**: The recursion stack depth is proportional to `target`.

---

## Solution Code

```cpp
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> result;
        vector<int> combination;
        backtrack(candidates, target, 0, combination, result);
        return result;
    }

private:
    void backtrack(vector<int>& candidates, int target, int start, vector<int>& combination, vector<vector<int>>& result) {
        if (target == 0) {
            result.push_back(combination);
            return;
        }
        if (target < 0) return;

        for (int i = start; i < candidates.size(); ++i) {
            combination.push_back(candidates[i]);
            backtrack(candidates, target - candidates[i], i, combination, result);
            combination.pop_back(); // backtrack
        }
    }
};
```

---

## Example Walkthrough

### Input: `candidates = [2,3,6,7]`, `target = 7`

1. Start with an empty combination and \( target = 7 \).
2. Explore recursively:
   - Include \( 2 \): Combination = [2], \( target = 5 \).
     - Include \( 2 \): Combination = [2, 2], \( target = 3 \).
       - Include \( 2 \): Combination = [2, 2, 2], \( target = 1 \) (terminate as \( target < 0 \)).
       - Include \( 3 \): Combination = [2, 2, 3], \( target = 0 \) (valid combination).
     - Skip \( 2 \), include \( 3 \), and so on.
3. Continue exploring other candidates recursively.

Output:
```plaintext
[[2, 2, 3], [7]]
```

---

## Edge Cases

1. **Empty Candidates**:
   - Input: `candidates = []`, `target = 5`.  
     Output: `[]`.

2. **Single Candidate Larger Than Target**:
   - Input: `candidates = [10]`, `target = 7`.  
     Output: `[]`.

3. **Multiple Solutions**:
   - Input: `candidates = [1, 2, 3]`, `target = 4`.  
     Output: `[[1, 1, 1, 1], [1, 1, 2], [1, 3], [2, 2]]`.
