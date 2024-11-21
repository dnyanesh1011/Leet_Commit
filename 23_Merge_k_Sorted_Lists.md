# ⛓️‍💥Merge k Sorted Lists

## Problem Statement

You are given an array of \( k \) linked lists, where each linked list is sorted in ascending order. Merge all the linked lists into one sorted linked list and return it.

---

## Examples

### Example 1:
**Input:**  
`lists = [[1,4,5],[1,3,4],[2,6]]`  
**Output:**  
`[1,1,2,3,4,4,5,6]`  

**Explanation:**  
The linked lists are:  
```
1 -> 4 -> 5  
1 -> 3 -> 4  
2 -> 6  
```
After merging, the result is:  
```
1 -> 1 -> 2 -> 3 -> 4 -> 4 -> 5 -> 6
```

---

### Example 2:
**Input:**  
`lists = []`  
**Output:**  
`[]`  

---

### Example 3:
**Input:**  
`lists = [[]]`  
**Output:**  
`[]`  

---

## Approach

1. **Priority Queue (Min-Heap)**:
   - Use a priority queue (min-heap) to always extract the smallest node from the current \( k \) nodes.

2. **Add Initial Nodes**:
   - Push the head of each linked list into the heap.

3. **Merge Process**:
   - Extract the smallest node from the heap and add it to the merged list.
   - If the extracted node has a next node, push it into the heap.

4. **Construct Result List**:
   - Use a dummy node to simplify appending nodes to the result list.

5. **Return the Result**:
   - Return the merged list starting from the node after the dummy.

---

## Solution Code

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    struct Compare {
        bool operator()(ListNode* a, ListNode* b) {
            return a->val > b->val; // minimum heap based on node values
        }
    };

    ListNode* mergeKLists(vector<ListNode*>& lists) {
        // minimum heap to store the smallest nodes from each list
        priority_queue<ListNode*, vector<ListNode*>, Compare> minHeap;

        // push the head of each list into the heap
        for (ListNode* list : lists) {
            if (list != nullptr) {
                minHeap.push(list);
            }
        }

        // duplicate node to simplify result list construction
        ListNode* dummy = new ListNode(0);
        ListNode* current = dummy;

        while (!minHeap.empty()) {
            // extract the smallest node from the heap
            ListNode* smallest = minHeap.top();
            minHeap.pop();

            // adding it to the result list
            current->next = smallest;
            current = current->next;

            // if the extracted node has a next node, push it into the heap
            if (smallest->next != nullptr) {
                minHeap.push(smallest->next);
            }
        }

        return dummy->next; // Return the head of the merged list
    }
};
```

---

## Complexity Analysis

### Time Complexity:
- **O(N log k)**, where \( N \) is the total number of nodes and \( k \) is the number of lists.  
  - Pushing and popping from the heap takes \( O(\log k) \).  
  - Each node is processed once.

### Space Complexity:
- **O(k)**, for the heap storing up to \( k \) nodes.

---

## Edge Cases to Consider

1. **Empty List of Lists**:
   - Input: `lists = []`  
   - Output: `[]`  

2. **Single Empty List**:
   - Input: `lists = [[]]`  
   - Output: `[]`  

3. **Single Non-Empty List**:
   - Input: `lists = [[1,2,3]]`  
   - Output: `[1,2,3]`  

4. **Lists with Different Lengths**:
   - Input: `lists = [[1],[2,3],[4,5,6]]`  
   - Output: `[1,2,3,4,5,6]`  

---

## Notes

This solution leverages a priority queue to efficiently merge \( k \) sorted lists while maintaining optimal time complexity. The use of a dummy node simplifies appending nodes to the result list. 🚀
