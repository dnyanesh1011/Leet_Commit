# ®️emove Nth Node From End of List

## Problem Statement

Given the head of a linked list, remove the \( n \)-th node from the end of the list and return its head.

---

## Examples

### Example 1:
**Input:**  
`head = [1,2,3,4,5], n = 2`  
**Output:**  
`[1,2,3,5]`  

**Explanation:**  
The 2nd node from the end is `4`. After removing it, the list becomes `[1,2,3,5]`.

---

### Example 2:
**Input:**  
`head = [1], n = 1`  
**Output:**  
`[]`  

**Explanation:**  
The list contains only one node, and removing it leaves an empty list.

---

### Example 3:
**Input:**  
`head = [1,2], n = 1`  
**Output:**  
`[1]`  

**Explanation:**  
The 1st node from the end is `2`. After removing it, the list becomes `[1]`.

---

## Approach

1. **Dummy Node**:
   - Create a dummy node pointing to the head to simplify edge cases (e.g., removing the first node).

2. **Two-Pointer Technique**:
   - Use two pointers (`first` and `second`), both initialized at the dummy node.
   - Move `first` pointer \( n+1 \) steps ahead to maintain a gap of \( n \) nodes between `first` and `second`.

3. **Traverse the List**:
   - Move both pointers one step at a time until `first` reaches the end. At this point, `second` points to the node just before the \( n \)-th node from the end.

4. **Remove the Node**:
   - Update `second->next` to skip the \( n \)-th node.

5. **Return the Result**:
   - Return `dummy->next`, which points to the updated head.

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        // create a dummy node pointing to the head to handle edge cases
        ListNode* dummy = new ListNode(0, head);
        ListNode* first = dummy;
        ListNode* second = dummy;

        // increasing the first pointer by n+1 steps to maintain a gap of n between first and second
        for (int i = 0; i <= n; ++i) {
            first = first->next;
        }

        // traversing both pointers until the first reaches the end
        while (first != nullptr) {
            first = first->next;
            second = second->next;
        }

        // eliminating the nth node from the end by skipping it
        second->next = second->next->next;

        // return the updated list starting from the original head
        return dummy->next;
    }
};
```

---

## Complexity Analysis

### Time Complexity:
- **O(L)**, where \( L \) is the length of the linked list.  
  The list is traversed twice: once to move the `first` pointer \( n+1 \) steps and again to remove the node.

### Space Complexity:
- **O(1)**, as no additional data structures are used.

---

## Edge Cases to Consider

1. **Single Node List**:
   - Input: `head = [1], n = 1`  
   - Output: `[]`  

2. **Remove the First Node**:
   - Input: `head = [1,2,3], n = 3`  
   - Output: `[2,3]`  

3. **List with Multiple Nodes**:
   - Input: `head = [1,2,3,4,5], n = 1`  
   - Output: `[1,2,3,4]`  

4. **Empty List**:
   - Input: `head = [], n = 1`  
   - Edge case: Not applicable since the list is always non-empty as per problem constraints.

---

## Notes

This solution efficiently removes the \( n \)-th node from the end of the list using a two-pointer technique, handling edge cases like removing the first or last node with ease. 🚀
