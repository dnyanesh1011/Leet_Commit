# 🪨 Moving Stones Until Consecutive II

## Problem Statement

You are given an array of integers `stones`, representing the positions of stones on the X-axis. In this problem, you can perform moves to reorganize the stones into consecutive positions. The game ends when the stones are arranged such that all positions are consecutive.

### Rules:
1. You can pick up an **endpoint stone** (the smallest or largest stone position) and move it to an unoccupied position, such that it is no longer an endpoint.
2. The goal is to calculate the **minimum** and **maximum** number of moves required to rearrange the stones.

---

### Examples

#### Example 1:
**Input:**  
`stones = [7,4,9]`  
**Output:**  
`[1,2]`  
**Explanation:**  
- Minimum moves: Move `4 → 8` to finish in 1 move.  
- Maximum moves: Move `9 → 5`, then `4 → 6` to finish in 2 moves.

#### Example 2:
**Input:**  
`stones = [6,5,4,3,10]`  
**Output:**  
`[2,3]`  
**Explanation:**  
- Minimum moves: Move `3 → 8`, then `10 → 7` to finish in 2 moves.  
- Maximum moves: Move `3 → 7`, `4 → 8`, and `5 → 9` to finish in 3 moves.

---

## Approach and Solution

The problem can be solved by:
1. **Sorting the Stones**: Sorting the stones ensures that their relative positions are in order for efficient calculation.
2. **Maximum Moves**:
   - The maximum moves are calculated as the total unoccupied positions between the smallest and largest stone (`stones[n-1] - stones[0] + 1 - n`), subtracting the largest gap between the first two and last two stones.
3. **Minimum Moves**:
   - Use a sliding window technique to calculate the minimum number of moves. This involves finding the largest window where all the stones can fit within `n` positions and minimizing moves to fill the rest.

---

## Solution Code

```cpp
class Solution {
public:
    vector<int> numMovesStonesII(vector<int>& stones) {
        sort(stones.begin(), stones.end());
        int n = stones.size();
        
        // Calculate max moves
        int maxMoves = stones[n - 1] - stones[0] + 1 - n;
        maxMoves -= min(stones[1] - stones[0] - 1, stones[n - 1] - stones[n - 2] - 1); 
        
        // Calculate min moves using sliding window
        int minMoves = n;
        int j = 0;
        for (int i = 0; i < n; ++i) {
            while (j < n && stones[j] - stones[i] + 1 <= n) {
                ++j;
            }
            int stonesInWindow = j - i;
            if (stonesInWindow == n - 1 && stones[j - 1] - stones[i] + 1 == n - 1) {
                minMoves = min(minMoves, 2); // Special case for one empty slot in the window
            } else {
                minMoves = min(minMoves, n - stonesInWindow);
            }
        }
        
        return {minMoves, maxMoves};
    }
};
```

---

## Complexity Analysis

### Time Complexity:
1. **Sorting the Stones**: **O(n log n)**.
2. **Sliding Window for Minimum Moves**: **O(n)**.
3. **Maximum Moves Calculation**: **O(1)**.

Overall time complexity: **O(n log n)**.

### Space Complexity:
- The space complexity is **O(1)**, as no extra space is used apart from variables.

---

## Examples to Test

1. **Small Case**:  
   Input: `stones = [1,2,5]`  
   Output: `[1,2]`  

2. **Single Gap at the Start**:  
   Input: `stones = [10,2,3,4,5]`  
   Output: `[1,4]`  

3. **Stones Already Consecutive**:  
   Input: `stones = [1,2,3,4,5]`  
   Output: `[0,0]`  

4. **Large Case with Gaps**:  
   Input: `stones = [1,3,6,10,15]`  
   Output: `[3,10]`  

---

## Conclusion

The solution efficiently calculates both the minimum and maximum moves required to rearrange stones into consecutive positions. By leveraging sorting and the sliding window technique, the algorithm maintains optimal time complexity while handling edge cases like large gaps and nearly consecutive stones.
