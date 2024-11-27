# 📋 Sort Linked List  

## Problem Statement  

You are given the head of a singly linked list. Your task is to sort the linked list in ascending order and return the sorted list. The solution must use \(O(n \log n)\) time complexity and \(O(1)\) space complexity (excluding the recursion stack).  

---

## Examples  

### Example 1  

**Input**:  
```plaintext  
head = [4, 2, 1, 3]  
```  
**Output**:  
```plaintext  
[1, 2, 3, 4]  
```  

### Example 2  

**Input**:  
```plaintext  
head = [-1, 5, 3, 4, 0]  
```  
**Output**:  
```plaintext  
[-1, 0, 3, 4, 5]  
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

### Merge Sort for Linked List  

The optimal approach to sort a linked list is to use **merge sort**.  

1. **Split the List**:  
   - Use the slow and fast pointer technique to find the middle node and split the list into two halves.  
   - Recursively sort each half.  

2. **Merge the Sorted Lists**:  
   - Use a helper function to merge two sorted linked lists into one sorted list.  

---

## Solution Code  

```cpp  
class Solution {  
public:  
    ListNode* sortList(ListNode* head) {  
        if (!head || !head->next) {  
            return head;  
        }  

        // Step 1: Find the middle of the list  
        ListNode* mid = findMiddle(head);  
        ListNode* rightHalf = mid->next;  
        mid->next = nullptr;  

        // Step 2: Recursively sort the left and right halves  
        ListNode* left = sortList(head);  
        ListNode* right = sortList(rightHalf);  

        // Step 3: Merge the two sorted halves  
        return merge(left, right);  
    }  

private:  
    // Helper function to find the middle of the linked list  
    ListNode* findMiddle(ListNode* head) {  
        ListNode* slow = head;  
        ListNode* fast = head->next;  

        while (fast && fast->next) {  
            slow = slow->next;  
            fast = fast->next->next;  
        }  
        return slow;  
    }  

    // Helper function to merge two sorted linked lists  
    ListNode* merge(ListNode* l1, ListNode* l2) {  
        ListNode dummy(0);  
        ListNode* current = &dummy;  

        while (l1 && l2) {  
            if (l1->val < l2->val) {  
                current->next = l1;  
                l1 = l1->next;  
            } else {  
                current->next = l2;  
                l2 = l2->next;  
            }  
            current = current->next;  
        }  

        // Append the remaining nodes  
        current->next = l1 ? l1 : l2;  

        return dummy.next;  
    }  
};  
```  

---

## Complexity Analysis  

- **Time Complexity**:  
  - \(O(n \log n)\): The list is divided into halves recursively (\(\log n\)) and merging takes \(O(n)\).  

- **Space Complexity**:  
  - \(O(1)\): Since no extra space is used (excluding the recursion stack).  

---

## Edge Cases  

1. **Empty List**:  
   Input: `head = []`  
   Output: `[]`  

2. **Single Element List**:  
   Input: `head = [1]`  
   Output: `[1]`  

3. **Already Sorted List**:  
   Input: `head = [1, 2, 3]`  
   Output: `[1, 2, 3]`  

4. **Reverse Sorted List**:  
   Input: `head = [3, 2, 1]`  
   Output: `[1, 2, 3]`  

---

## Conclusion  

This solution effectively sorts a linked list in \(O(n \log n)\) time complexity using the merge sort algorithm, which is well-suited for linked lists due to their sequential access nature.
