# 🔄 Reorder List  

## Problem Statement  

Given the head of a singly linked list:  
\[ L_0 \rightarrow L_1 \rightarrow \dots \rightarrow L_{n-1} \rightarrow L_n \],  

reorder it to the following form:  
\[ L_0 \rightarrow L_n \rightarrow L_1 \rightarrow L_{n-1} \rightarrow L_2 \rightarrow L_{n-2} \dots \].  

- **Constraints**:  
  - You may not modify the values in the list's nodes.
  - Only the node pointers can be changed.  

---

## Examples  

### Example 1  

**Input**:  
```plaintext  
head = [1,2,3,4]  
```  
**Output**:  
```plaintext  
[1,4,2,3]  
```  

### Example 2  

**Input**:  
```plaintext  
head = [1,2,3,4,5]  
```  
**Output**:  
```plaintext  
[1,5,2,4,3]  
```  

---

## Approach  

### Steps  

1. **Find the Middle of the List**:  
   - Use the **slow and fast pointer technique** to find the middle node.  

2. **Reverse the Second Half of the List**:  
   - Reverse the list starting from the middle to the end.  

3. **Merge the Two Halves**:  
   - Alternate nodes from the first half and the reversed second half.  

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
    void reorderList(ListNode* head) {  
        if (!head || !head->next) return;  

        // Step 1: Find the middle of the list  
        ListNode* slow = head;  
        ListNode* fast = head;  
        while (fast->next && fast->next->next) {  
            slow = slow->next;  
            fast = fast->next->next;  
        }  

        // Step 2: Reverse the second half of the list  
        ListNode* second = reverseList(slow->next);  
        slow->next = nullptr;  

        // Step 3: Merge the two halves  
        ListNode* first = head;  
        while (second) {  
            ListNode* temp1 = first->next;  
            ListNode* temp2 = second->next;  

            first->next = second;  
            second->next = temp1;  

            first = temp1;  
            second = temp2;  
        }  
    }  

private:  
    ListNode* reverseList(ListNode* head) {  
        ListNode* prev = nullptr;  
        while (head) {  
            ListNode* next = head->next;  
            head->next = prev;  
            prev = head;  
            head = next;  
        }  
        return prev;  
    }  
};  
```  

---

## Complexity Analysis  

### Time Complexity  
- **O(n)**:  
  - Finding the middle: \(O(n)\).  
  - Reversing the second half: \(O(n/2)\).  
  - Merging: \(O(n)\).  

### Space Complexity  
- **O(1)**: No extra space used.  

---

## Edge Cases  

1. **Empty List**:  
   Input: `head = []`  
   Output: `[]`  

2. **Single Node List**:  
   Input: `head = [1]`  
   Output: `[1]`  

3. **Two Nodes List**:  
   Input: `head = [1,2]`  
   Output: `[1,2]`  

---

## Explanation  

1. **Find the Middle**:  
   - Use slow and fast pointers to split the list into two halves.  

2. **Reverse the Second Half**:  
   - Reverse the list from the middle to the end.  

3. **Merge**:  
   - Interleave nodes from the first and reversed second halves.  

---

## Visualization  

### Input: `head = [1,2,3,4,5]`  

1. **Find Middle**:  
   - First Half: \([1,2,3]\)  
   - Second Half: \([4,5]\)  

2. **Reverse Second Half**:  
   - Reversed Second Half: \([5,4]\)  

3. **Merge**:  
   - \([1,5,2,4,3]\)  

This approach maintains the required ordering while adhering to the constraints.
