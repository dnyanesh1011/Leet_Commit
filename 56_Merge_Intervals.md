# Merge Intervals

## Problem Description

Given an array of intervals `intervals` where `intervals[i] = [start_i, end_i]`, merge all overlapping intervals and return an array of the non-overlapping intervals that cover all the intervals in the input.

---

## Examples

### Example 1:
**Input**:  
```plaintext
intervals = [[1,3],[2,6],[8,10],[15,18]]
```  

**Output**:  
```plaintext
[[1,6],[8,10],[15,18]]
```  

**Explanation**:  
- Intervals [1,3] and [2,6] overlap, so they are merged into [1,6].

---

### Example 2:
**Input**:  
```plaintext
intervals = [[1,4],[4,5]]
```  

**Output**:  
```plaintext
[[1,5]]
```  

**Explanation**:  
- Intervals [1,4] and [4,5] overlap, so they are merged into [1,5].

---

## Approach

### Key Insights

1. **Sorting by Start Time**:
   - Sorting ensures that intervals are processed in ascending order of their start times, which simplifies merging.

2. **Overlapping Check**:
   - Two intervals overlap if:
     \[
     \text{current.start} \leq \text{previous.end}
     \]
   - If overlapping, the intervals are merged:
     \[
     \text{merged.end} = \max(\text{previous.end}, \text{current.end})
     \]

3. **No Overlap**:
   - If two intervals do not overlap, the current interval is added to the result as a new merged interval.

---

## Solution Steps

1. **Sort the Input**:
   - Sort the intervals based on their start times.

2. **Initialize Result List**:
   - Create an empty list to store merged intervals.

3. **Iterate Through Intervals**:
   - For each interval:
     - If the list is empty or the current interval does not overlap with the last merged interval, add it as a new interval.
     - Otherwise, merge the intervals by updating the end of the last merged interval.

4. **Return the Result**:
   - After processing all intervals, return the merged list.

---

## Complexity Analysis

### Time Complexity
- **Sorting**: \(O(n \log n)\), where \(n\) is the number of intervals.
- **Iteration**: \(O(n)\), for processing the intervals.  
**Overall**: \(O(n \log n)\)

### Space Complexity
- \(O(n)\), for storing the merged intervals.

---

## Solution Code

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        // Step 1: Sort intervals based on start time
        sort(intervals.begin(), intervals.end());
        
        vector<vector<int>> merged;
        
        // Step 2: Iterate through intervals
        for (const auto& interval : intervals) {
            // If no overlap, add the interval to the result
            if (merged.empty() || merged.back()[1] < interval[0]) {
                merged.push_back(interval);
            } else {
                // If overlap, merge the intervals
                merged.back()[1] = max(merged.back()[1], interval[1]);
            }
        }
        
        return merged;
    }
};
```

---

## Example Walkthrough

### Input: `intervals = [[1,3],[2,6],[8,10],[15,18]]`

1. **Sort the Intervals**:  
   \[
   [[1,3],[2,6],[8,10],[15,18]]
   \]

2. **Iterate Through the Intervals**:
   - Start with `merged = []`.

   - Process `[1,3]`:  
     \[
     \text{merged} = [[1,3]]
     \]

   - Process `[2,6]`:  
     Overlap with `[1,3]`, merge into `[1,6]`.  
     \[
     \text{merged} = [[1,6]]
     \]

   - Process `[8,10]`:  
     No overlap, add to result.  
     \[
     \text{merged} = [[1,6],[8,10]]
     \]

   - Process `[15,18]`:  
     No overlap, add to result.  
     \[
     \text{merged} = [[1,6],[8,10],[15,18]]
     \]

3. **Return Merged Intervals**:
   \[
   [[1,6],[8,10],[15,18]]
   \]

---

## Edge Cases

1. **Empty Input**:
   - Input: `intervals = []`
   - Output: `[]`

2. **Single Interval**:
   - Input: `intervals = [[1,2]]`
   - Output: `[[1,2]]`

3. **Non-Overlapping Intervals**:
   - Input: `intervals = [[1,2],[3,4],[5,6]]`
   - Output: `[[1,2],[3,4],[5,6]]`

4. **Fully Overlapping Intervals**:
   - Input: `intervals = [[1,10],[2,6],[3,8]]`
   - Output: `[[1,10]]`
