# Sort an Array

## Problem Statement

The task is to implement a function that sorts an array of integers using the **Merge Sort** algorithm, which has a time complexity of **O(n log n)** and is known for its efficiency in sorting large datasets. The function should return the sorted array.

### Input:
- A vector `nums` containing integers to be sorted.

### Output:
- A vector containing the sorted integers.

### Constraints:
- The input array `nums` may contain distinct integers.
- The function must return a sorted version of the input array.

## Approach and Solution Explanation

### Algorithm Overview:
**Merge Sort** is a **divide-and-conquer** algorithm that splits the array into two halves, recursively sorts each half, and then merges the sorted halves back together. This ensures that the time complexity remains optimal at **O(n log n)**, even in the worst case.

### Detailed Explanation:

1. **Dividing the Array**: 
   - The array is recursively divided into two halves until each subarray has one or zero elements. Each division is based on calculating the middle index (`mid`).

2. **Merging Sorted Halves**:
   - Once the array is divided, each pair of subarrays is merged back together. During the merge step, the elements from two sorted subarrays are compared and placed in the correct order to form a sorted array.

3. **Merge Function**:
   - The `merge` function takes two sorted subarrays and merges them into one sorted subarray. The elements are picked from both subarrays and placed in the correct order, ensuring the merged array is sorted.

4. **Recursive Sort**:
   - The `mergeSort` function calls itself recursively to sort the two halves of the array. After sorting both halves, it calls the `merge` function to combine the sorted halves into a single sorted array.

### Code Implementation:

```cpp
class Solution {
public:
    // Merge two sorted halves
    void merge(vector<int>& nums, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;
        
        vector<int> leftArr(n1), rightArr(n2);
        
        // Copy data to temp arrays leftArr[] and rightArr[]
        for (int i = 0; i < n1; i++)
            leftArr[i] = nums[left + i];
        for (int i = 0; i < n2; i++)
            rightArr[i] = nums[mid + 1 + i];
        
        // Merge the temp arrays back into nums[left..right]
        int i = 0, j = 0, k = left;
        while (i < n1 && j < n2) {
            if (leftArr[i] <= rightArr[j]) {
                nums[k] = leftArr[i];
                i++;
            } else {
                nums[k] = rightArr[j];
                j++;
            }
            k++;
        }
        
        // Copy remaining elements of leftArr[]
        while (i < n1) {
            nums[k] = leftArr[i];
            i++;
            k++;
        }
        
        // Copy remaining elements of rightArr[]
        while (j < n2) {
            nums[k] = rightArr[j];
            j++;
            k++;
        }
    }

    // Main merge sort function
    void mergeSort(vector<int>& nums, int left, int right) {
        if (left < right) {
            int mid = left + (right - left) / 2;

            // Recursively sort the two halves
            mergeSort(nums, left, mid);
            mergeSort(nums, mid + 1, right);

            // Merge the sorted halves
            merge(nums, left, mid, right);
        }
    }

    // Function to sort the entire array
    vector<int> sortArray(vector<int>& nums) {
        mergeSort(nums, 0, nums.size() - 1);
        return nums;
    }
};
```

### How It Works:
1. **`merge` Function**: This function merges two sorted subarrays into one sorted array. It compares the elements from the left and right subarrays and places the smaller element in the correct position of the original array.

2. **`mergeSort` Function**: This function recursively splits the array into two halves, sorts them individually, and then merges them back into one sorted array using the `merge` function.

3. **`sortArray` Function**: This is the entry point of the sorting process, calling the `mergeSort` function on the entire array.

### Time and Space Complexity:

- **Time Complexity**:
  - **Best, Average, Worst Case**: **O(n log n)**. 
    - The array is repeatedly divided in half (log n splits), and each split involves a linear pass to merge the subarrays (n comparisons).
  
- **Space Complexity**:
  - **O(n)**. The auxiliary space is required to store temporary arrays (`leftArr` and `rightArr`) used in the merge step.

### Edge Cases:
1. **Empty Array**:
   - Input: `nums = []`
   - Output: `[]`
   
2. **Array with One Element**:
   - Input: `nums = [5]`
   - Output: `[5]`
   
3. **Array with Multiple Identical Elements**:
   - Input: `nums = [5, 5, 5, 5]`
   - Output: `[5, 5, 5, 5]` (array remains unchanged as it's already sorted).

4. **Array with Random Integers**:
   - Input: `nums = [4, 2, 7, 1, 3]`
   - Output: `[1, 2, 3, 4, 7]` (sorted array).


## Conclusion

This solution provides an efficient sorting mechanism using **Merge Sort**, which is well-suited for large datasets. It ensures an **O(n log n)** time complexity and leverages the divide-and-conquer principle to handle sorting in an optimal manner. The space complexity is **O(n)** due to the extra space required for merging the arrays.
