# 🚧🚧Maximum Gap

## Problem Statement

The problem asks to find the **maximum gap** between two successive elements in a sorted array that has been rotated. The goal is to return the maximum difference between two adjacent numbers in the sorted form of the array. If the array contains fewer than two elements, return `0`.

The solution must run in **O(n)** time and use **O(n)** extra space, where `n` is the number of elements in the input array.

### Input:
- An integer array `nums`.

### Output:
- The maximum gap between two successive elements in the sorted form of the array. If the array has fewer than two elements, return 0.

### Constraints:
- The input array `nums` will contain distinct integers.

### Example 1:
```cpp
Input:  [3,6,9,1]
Output: 3
Explanation: The sorted form of the array is [1, 3, 6, 9]. The maximum gap is between 6 and 9 or between 3 and 6, both of which are 3.
```

### Example 2:
```cpp
Input: [10]
Output: 0
Explanation: The array contains fewer than two elements, so the result is 0.
```

## Approach and Solution Explanation

### Problem Breakdown:
To find the maximum gap between two successive elements, we can use an efficient approach based on **bucket sorting**. This method ensures that we find the maximum gap in **O(n)** time complexity, with **O(n)** extra space.

### Steps:
1. **Edge Case**:
   - If the array contains fewer than two elements, return `0` because there are no adjacent elements.

2. **Find Minimum and Maximum Values**:
   - Calculate the minimum (`minNum`) and maximum (`maxNum`) values in the array.

3. **Determine Bucket Size**:
   - Calculate the bucket size as `(maxNum - minNum) / (n - 1)`. This ensures that the difference between the elements in the same bucket is minimized.

4. **Distribute Elements into Buckets**:
   - We divide the array elements into buckets such that the elements in each bucket are as close to each other as possible.
   - Each bucket stores two values: the minimum and maximum value of the elements assigned to that bucket.

5. **Calculate Maximum Gap**:
   - After distributing the elements into buckets, the largest gap will be found between the maximum value of one bucket and the minimum value of the next non-empty bucket.

6. **Return the Maximum Gap**:
   - Iterate through the buckets and calculate the gap between the maximum value of one bucket and the minimum value of the next non-empty bucket.

### Solution Code:

```cpp
#include <vector>
#include <algorithm>
#include <climits>

class Solution {
public:
    int maximumGap(std::vector<int>& nums) {
        if (nums.size() < 2) return 0;
        
        // Find the min and max values in the array
        int minNum = *std::min_element(nums.begin(), nums.end());
        int maxNum = *std::max_element(nums.begin(), nums.end());
        
        // size of each bucket
        int n = nums.size();
        int bucketSize = std::max(1, (maxNum - minNum) / (n - 1));  // Avoid division by zero
        int bucketCount = (maxNum - minNum) / bucketSize + 1;
        
        // create buckets to store the min and max values in each bucket
        std::vector<std::pair<int, int>> buckets(bucketCount, {INT_MAX, INT_MIN});
        
        // distribute the numbers into buckets
        for (int num : nums) {
            int index = (num - minNum) / bucketSize;
            buckets[index].first = std::min(buckets[index].first, num);
            buckets[index].second = std::max(buckets[index].second, num);
        }
        
        // find the maximum gap
        int maxGap = 0;
        int previousMax = minNum;
        
        for (const auto& bucket : buckets) {
            if (bucket.first == INT_MAX) continue;  // Skip empty buckets
            
            maxGap = std::max(maxGap, bucket.first - previousMax);
            previousMax = bucket.second;
        }
        
        return maxGap;
    }
};
```

## Time and Space Complexity

### Time Complexity:
- **O(n)**: The solution runs in linear time because:
  - We compute the minimum and maximum values in the array in **O(n)**.
  - We distribute the elements into buckets in **O(n)**.
  - We compute the maximum gap by iterating over the buckets in **O(n)**.

### Space Complexity:
- **O(n)**: We use extra space for the buckets, which is proportional to the number of elements in the array.

## Edge Cases to Consider:
1. **Array with Less Than Two Elements**:
   - Input: `nums = [1]`
   - Output: `0` (No gap between elements).

2. **Array with Large Gaps**:
   - Input: `nums = [1, 1000000]`
   - Output: `999999` (The only possible gap is the difference between 1 and 1000000).

3. **Array with Multiple Consecutive Numbers**:
   - Input: `nums = [1, 2, 3, 4, 5]`
   - Output: `1` (The gap between each successive number is 1).

4. **Array with Identical Numbers**:
   - Input: `nums = [5, 5, 5, 5]`
   - Output: `0` (No gap between identical numbers).

## Conclusion

This solution efficiently computes the maximum gap between successive elements in a sorted array (that might be rotated) using the bucket sort technique. The approach ensures an optimal time complexity of **O(n)**, making it suitable for large input sizes while adhering to the problem's constraints of linear time and space complexity.
