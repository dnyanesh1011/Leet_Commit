# ➕Add Two Numbers

## Problem Statement

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number `0` itself.

---

## Examples

### Example 1:
**Input:**  
`list1 = [2,4,3], list2 = [5,6,4]`  
**Output:**  
`[7,0,8]`  

**Explanation:**  
342 + 465 = 807 (stored as `[7,0,8]` in reverse order).

---

### Example 2:
**Input:**  
`list1 = [0], list2 = [0]`  
**Output:**  
`[0]`  

---

### Example 3:
**Input:**  
`list1 = [9,9,9,9,9,9,9], list2 = [9,9,9,9]`  
**Output:**  
`[8,9,9,9,0,0,0,1]`  

**Explanation:**  
9999999 + 9999 = 10009998 (stored as `[8,9,9,9,0,0,0,1]` in reverse order).

---

## Approach

1. **Iterate Through Both Lists**:
   - Traverse both linked lists until all nodes and carry are processed.

2. **Sum Corresponding Digits**:
   - Add the values of the nodes from both lists along with any carry from the previous step.

3. **Compute Carry and Remainder**:
   - Calculate the new carry as the integer division of the sum by 10.
   - Use the remainder as the value for the current node.

4. **Construct the Result List**:
   - Use a dummy node to simplify appending new nodes to the result linked list.

5. **Return the Result**:
   - Return the list starting from the node after the dummy.

---

## Solution Code

```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* list1, ListNode* list2) {
        ListNode* dummyHead = new ListNode(0); // dummy node to simplify code
        ListNode* current = dummyHead;
        int carry = 0;

        // iterating through both lists until we reach the end of both
        while (list1 != nullptr || list2 != nullptr || carry != 0) {
            int sum = carry;

            // adding the value from list1, if it exists
            if (list1 != nullptr) {
                sum += list1->val;
                list1 = list1->next;
            }

            // adding the value from list2, if it exists
            if (list2 != nullptr) {
                sum += list2->val;
                list2 = list2->next;
            }

            // compute new carry and the value to store in the node
            carry = sum / 10;
            int value = sum % 10;

            // add the new node to the result list
            current->next = new ListNode(value);
            current = current->next;
        }

        return dummyHead->next; // return the result list
    }
};
```

---

## Complexity Analysis

### Time Complexity:
- **O(max(n, m))**, where \(n\) and \(m\) are the lengths of `list1` and `list2`, respectively.  
  Each list is traversed once.

### Space Complexity:
- **O(max(n, m))**, for the resulting linked list.

---

## Edge Cases to Consider

1. **Different Lengths of Lists**:
   - Input: `list1 = [2,4], list2 = [5,6,4]`  
   - Output: `[7,0,5]`  

2. **Carry at the End**:
   - Input: `list1 = [9,9,9], list2 = [1]`  
   - Output: `[0,0,0,1]`  

3. **Empty Lists**:
   - Input: `list1 = [], list2 = []`  
   - Output: `[]`  

4. **One Empty List**:
   - Input: `list1 = [2,4,3], list2 = []`  
   - Output: `[2,4,3]`  

---

## Notes

This implementation simplifies addition of two numbers represented as linked lists, leveraging modular arithmetic for node values and carry propagation. 🚀
