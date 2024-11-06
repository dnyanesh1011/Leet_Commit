# 🧠 Problem Title: Median of Two Sorted Arrays

## Problem Statement
Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return the median of the two sorted arrays.

The overall runtime complexity should be O(log (m+n)).

### Example 1:
**Input**: 
```cpp
nums1 = [1,3], nums2 = [2]
```
**Output**:
```cpp
2.00000
```
**Explanation**: The merged array is `[1, 2, 3]` and the median is `2`.

### Example 2:
**Input**:
```cpp
nums1 = [1,2], nums2 = [3,4]
```
**Output**:
```cpp
2.50000
```
**Explanation**: The merged array is `[1, 2, 3, 4]` and the median is `(2 + 3) / 2 = 2.5`.

## Approach and Solution Explanation

The solution uses binary search to partition the two sorted arrays. By adjusting the partitions, we are able to find the median in logarithmic time. Here is how the approach works:

1. **Partitioning**: 
   We divide the two arrays into two parts such that the left part contains elements smaller than the elements in the right part.
   - We find the correct partition by checking the left and right bounds of both arrays.
   - The partition is chosen such that the left partition contains half of the total elements, and the right partition contains the other half.

2. **Binary Search**:
   - Perform binary search on the smaller array to determine the correct partition, and then calculate the corresponding partition in the larger array.
   - Based on the values around the partitions, determine if the partition is correct.

3. **Median Calculation**:
   - If the combined total length of the two arrays is odd, the median is the maximum of the left elements.
   - If the combined total length is even, the median is the average of the maximum left element and the minimum right element.

### Steps:
1. **Ensure nums1 is the smaller array**: We swap the arrays if `nums1` is larger than `nums2` to minimize the binary search space.
2. **Binary Search Loop**: We search the smaller array and adjust the partitions until the correct one is found.
3. **Return the Median**: Once the correct partition is found, calculate the median based on the partition values.

## Complexity Analysis:
- **Time Complexity**: O(log(min(m, n))), where `m` and `n` are the sizes of `nums1` and `nums2`. The binary search is performed on the smaller array, which ensures that the time complexity is logarithmic in terms of the smaller array's size.
- **Space Complexity**: O(1), as we are using only a constant amount of extra space for the partitioning variables and calculations.

## Solution Code

```cpp
class Solution
{
public:
    double findMedianSortedArrays(vector<int> &nums1, vector<int> &nums2)
    {
        // Ensure nums1 is the smaller array
        if (nums1.size() > nums2.size())
            return findMedianSortedArrays(nums2, nums1);

        int m = nums1.size();
        int n = nums2.size();
        int left = 0, right = m;

        // Declare the boundary variables
        int maxLeft1, minRight1, maxLeft2, minRight2;

        while (left <= right)
        {
            int partition1 = (left + right) / 2;
            int partition2 = (m + n + 1) / 2 - partition1;

            // Set max/min for each partition edge case (out of bounds)
            // Check for maxLeft1
            if (partition1 == 0)
            {
                maxLeft1 = INT_MIN;
            }
            else
            {
                maxLeft1 = nums1[partition1 - 1];
            }

            // Check for minRight1
            if (partition1 == m)
            {
                minRight1 = INT_MAX;
            }
            else
            {
                minRight1 = nums1[partition1];
            }

            // Check for maxLeft2
            if (partition2 == 0)
            {
                maxLeft2 = INT_MIN;
            }
            else
            {
                maxLeft2 = nums2[partition2 - 1];
            }

            // Check for minRight2
            if (partition2 == n)
            {
                minRight2 = INT_MAX;
            }
            else
            {
                minRight2 = nums2[partition2];
            }

            // Check if partitions are correct
            if (maxLeft1 <= minRight2 && maxLeft2 <= minRight1)
            {
                // If total length is odd
                if ((m + n) % 2 == 1)
                {
                    return max(maxLeft1, maxLeft2);
                }
                else
                { // If total length is even
                    return (max(maxLeft1, maxLeft2) + min(minRight1, minRight2)) / 2.0;
                }
            }
            else if (maxLeft1 > minRight2)
            {
                right = partition1 - 1; // Move left in nums1
            }
            else
            {
                left = partition1 + 1; // Move right in nums1
            }
        }

        throw invalid_argument("Input arrays are not sorted.");
    }
};
```

## Conclusion
This solution efficiently finds the median of two sorted arrays using binary search, ensuring a time complexity of O(log(min(m, n))). This approach avoids the need to merge the arrays, making it optimal for large datasets.
