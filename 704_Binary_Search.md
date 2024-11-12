# 🔎Binary Search Algorithm in C++

## Overview
This C++ program implements a binary search algorithm to find the index of a target value within a sorted vector of integers. Binary search is a classic algorithm that efficiently locates an element in a sorted array by dividing the search interval in half, making it much faster than linear search for large datasets. This code uses a recursive helper function to perform the binary search.

## Features
- **Recursive Binary Search**: The `binarySearch` function is implemented recursively to divide the search range into halves until the target element is found or the search range is exhausted.
- **Efficiency**: This approach has a logarithmic time complexity of \(O(\log n)\), making it ideal for large sorted datasets.
- **Simple Interface**: The main `search` function is easy to use and encapsulates the recursive binary search logic.

## How to Use
1. **Initialize** the class `Solution`.
2. **Call the `search` method** with a sorted vector of integers (`nums`) and the `target` integer to find.
3. **Result**: The function returns the index of `target` if found; otherwise, it returns `-1`.

## Code

```cpp
#include <vector>
using namespace std;

class Solution {
public:
    int search(vector<int>& nums, int target) {
        return binarySearch(nums, 0, nums.size() - 1, target);
    }
    
private:
    // Recursive binary search helper function
    int binarySearch(const vector<int>& arr, int s, int e, int target) {
        // Base case: element not found
        if (s > e) {
            return -1;
        }

        int mid = s + (e - s) / 2;

        // Element found
        if (arr[mid] == target) {
            return mid;
        }
        
        // Recursive calls based on comparison
        if (arr[mid] < target) {
            return binarySearch(arr, mid + 1, e, target);
        } else {
            return binarySearch(arr, s, mid - 1, target);
        }
    }
};
```

## Explanation of Key Functions

### `search(vector<int>& nums, int target)`
This is the primary function to search for the target element in a sorted vector. It initializes the binary search with the full range of indices.

### `binarySearch(const vector<int>& arr, int s, int e, int target)`
A helper function that performs the recursive binary search:
1. **Base Case**: If the start index `s` exceeds the end index `e`, the element is not found, and `-1` is returned.
2. **Calculate Middle Index**: The middle index `mid` is computed, and `arr[mid]` is compared to the `target`.
3. **Recursive Calls**: Based on whether `arr[mid]` is less than or greater than `target`, the function either searches in the left or right half of the array.

## Example Usage

```cpp
int main() {
    Solution solution;
    vector<int> nums = {-10, -3, 0, 5, 9, 12};
    int target = 9;
    int result = solution.search(nums, target);
    // result will be 4, since nums[4] == 9
    return 0;
}
```

## Complexity Analysis

- **Time Complexity**: \(O(\log n)\), since binary search divides the search range in half with each recursive call.
- **Space Complexity**: \(O(\log n)\) in the worst case, due to the recursive function calls consuming stack space.

## Edge Cases Considered
- **Target not present**: Returns `-1` if the `target` is not in the array.
- **Empty vector**: An empty input vector will return `-1`.
- **Single-element vector**: Correctly returns the index if the target is present, `-1` otherwise.
- **Repeated elements**: This function will return the index of the first occurrence of `target` found in a standard binary search fashion.

