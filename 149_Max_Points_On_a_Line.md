# Max Points on a Line 📈

## Problem Description

You are given an array of points, where `points[i] = [xi, yi]` represents a point on the X-Y plane. Your task is to return the **maximum number of points** that lie on the same straight line.

---

## Examples

### Example 1:  
**Input**:  
```plaintext
points = [[1,1],[2,2],[3,3]]
```  
**Output**:  
```plaintext
3
```  
**Explanation**:  
All three points lie on the same line.

---

### Example 2:  
**Input**:  
```plaintext
points = [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]
```  
**Output**:  
```plaintext
4
```  
**Explanation**:  
The points `[1,1], [3,2], [5,3], [4,1]` lie on the same straight line.

---

## Approach and Solution Explanation

### Key Insights

1. **Line Equation**:
   - Any two points can define a straight line.
   - The slope of a line is a key determinant of collinearity. Points with the same slope relative to a reference point lie on the same line.

2. **HashMap for Slopes**:
   - Use a hashmap to count the frequency of slopes relative to a reference point.
   - The key of the hashmap is the slope, and the value is the count of points sharing that slope.

3. **Handling Precision**:
   - Use fractions (or reduced ratios) to represent slopes to avoid precision errors from floating-point division.

4. **Edge Cases**:
   - Duplicate points: These should be handled separately, as they don't affect the slope.
   - Vertical and horizontal lines: Represent these slopes distinctly (e.g., "infinity" for vertical lines).

---

### Algorithm

1. **Iterate Over Points**:
   - For each point, treat it as the reference point.

2. **Calculate Slopes**:
   - For every other point, calculate the slope relative to the reference point using reduced fractions.

3. **Count Slopes**:
   - Store the slopes in a hashmap, tracking how many points share each slope.

4. **Update Maximum**:
   - The maximum number of points for each reference point is the highest slope count plus the duplicates.

5. **Return Result**:
   - Return the overall maximum.

---

## Complexity Analysis

### Time Complexity
- **\(O(n^2)\)**:  
  - For each point, we compute the slopes relative to all other points (\(O(n)\)).

### Space Complexity
- **\(O(n)\)**:  
  - Hashmap stores slopes for each point.

---

## Solution Code

```cpp
#include <vector>
#include <unordered_map>
#include <algorithm>
#include <cmath>
#include <utility>

using namespace std;

class Solution {
public:
    int maxPoints(vector<vector<int>>& points) {
        int n = points.size();
        if (n <= 2) return n;

        int maxPointsOnLine = 0;

        for (int i = 0; i < n; ++i) {
            unordered_map<string, int> slopeMap;
            int duplicate = 1; // Count the reference point itself
            int currentMax = 0;

            for (int j = 0; j < n; ++j) {
                if (i == j) continue;

                int dx = points[j][0] - points[i][0];
                int dy = points[j][1] - points[i][1];

                if (dx == 0 && dy == 0) {
                    // Handle duplicate points
                    duplicate++;
                } else {
                    // Reduce slope to its simplest form
                    int gcdVal = gcd(dx, dy);
                    dx /= gcdVal;
                    dy /= gcdVal;

                    // Normalize direction of slope
                    if (dx < 0) {
                        dx = -dx;
                        dy = -dy;
                    } else if (dx == 0) {
                        dy = abs(dy);
                    }

                    string slope = to_string(dx) + "/" + to_string(dy);
                    slopeMap[slope]++;
                    currentMax = max(currentMax, slopeMap[slope]);
                }
            }

            maxPointsOnLine = max(maxPointsOnLine, currentMax + duplicate);
        }

        return maxPointsOnLine;
    }

private:
    int gcd(int a, int b) {
        return b == 0 ? a : gcd(b, a % b);
    }
};
```

---

## Example Walkthrough

### Input: `points = [[1,1],[2,2],[3,3]]`

1. **Reference Point: `[1,1]`**
   - Slopes:  
     - With `[2,2]`: \(1/1 = "1/1"\).  
     - With `[3,3]`: \(2/2 = "1/1"\).
   - Counts: `"1/1": 2`.  

2. **Add Duplicates**:
   - Maximum for `[1,1]`: \(2 + 1 = 3\).

3. **Repeat for Other Points**:
   - All points result in the same maximum.

**Output**: `3`

---

## Edge Cases

1. **Duplicate Points**:
   - Input: `points = [[1,1],[1,1],[2,2]]`
   - Output: `3` (all points are considered on the same line).

2. **Vertical Line**:
   - Input: `points = [[1,1],[1,2],[1,3]]`
   - Output: `3` (vertical slope).

3. **Horizontal Line**:
   - Input: `points = [[1,1],[2,1],[3,1]]`
   - Output: `3` (horizontal slope).

4. **Single Point**:
   - Input: `points = [[1,1]]`
   - Output: `1`.
