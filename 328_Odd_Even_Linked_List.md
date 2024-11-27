# 🔢 Odd Even Linked List  

## Problem Statement  

Given the head of a singly linked list, reorder the list such that all nodes at **odd indices** appear first, followed by all nodes at **even indices**. Maintain the relative order within the odd and even groups.  

You must solve the problem in \(O(1)\) space complexity and \(O(n)\) time complexity.  

---

## Examples  

### Example 1  

**Input**:  
```plaintext  
head = [1, 2, 3, 4, 5]  
```  
**Output**:  
```plaintext  
[1, 3, 5, 2, 4]  
```  

### Example 2  

**Input**:  
```plaintext  
head = [2, 1, 3, 5, 6, 4, 7]  
```  
**Output**:  
```plaintext  
[2, 3, 6, 7, 1, 5, 4]  
```  

### Example 3  

**Input**:  
```plaintext  
head = []  
```  
**Output**:  
```plaintext  
[]  
```  

---

## Approach and Explanation  

### Reordering the List  

1. Separate the list into two parts:  
   - Nodes at **odd indices**.  
   - Nodes at **even indices**.  

2. Use two pointers:  
   - **odd**: Tracks the current odd-index node.  
   - **even**: Tracks the current even-index node.  

3. **Iterate through the list**:  
   - Link the current odd node to the next odd-index node.  
   - Link the current even node to the next even-index node.  

4. Finally, connect the last odd node to the head of the even list.  

---

## Solution Code  

```cpp  
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {  
public:  
    ListNode* oddEvenList(ListNode* head) {  
        if (!head || !head->next) {  
            return head;  
        }  

        ListNode* odd = head;  
        ListNode* even = head->next;  
        ListNode* evenHead = even;  

        while (even && even->next) {  
            // Connect odd nodes  
            odd->next = even->next;  
            odd = odd->next;  

            // Connect even nodes  
            even->next = odd->next;  
            even = even->next;  
        }  

        // Link the end of odd list to the head of even list  
        odd->next = evenHead;  
        return head;  
    }  
};  
```  

---

## Complexity Analysis  

- **Time Complexity**:  
  - \(O(n)\): Traverse the list once to reorder it.  

- **Space Complexity**:  
  - \(O(1)\): No additional space is used apart from pointers.  

---

## Edge Cases  

1. **Empty List**:  
   Input: `head = []`  
   Output: `[]`  

2. **Single Node**:  
   Input: `head = [1]`  
   Output: `[1]`  

3. **Two Nodes**:  
   Input: `head = [1, 2]`  
   Output: `[1, 2]`  

4. **All Odd Nodes Only**:  
   Input: `head = [1, 3, 5]`  
   Output: `[1, 3, 5]`  

5. **All Even Nodes Only**:  
   Input: `head = [2, 4, 6]`  
   Output: `[2, 4, 6]`  

---

## Conclusion  

This solution effectively reorders the list into odd-index and even-index nodes in \(O(n)\) time and \(O(1)\) space. It preserves the relative order within both the odd and even groups.
