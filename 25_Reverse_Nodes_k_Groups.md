# 🔄 Reverse Nodes in k-Group

## Overview
This C++ program provides a solution to reverse the nodes of a singly linked list in groups of `k`. The program traverses the linked list, reversing nodes within each group of size `k` and leaving any remaining nodes (if their count is less than `k`) as they are.

## Features
- **Group-Based Reversal**: Reverses the nodes in groups of size `k` while maintaining the relative order of the groups.
- **In-Place Operation**: Reverses the nodes without using additional memory for another list.
- **Handles Edge Cases**: Works efficiently for cases where the total number of nodes is less than `k` or not a multiple of `k`.

## Code

```cpp
class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        if (!head || k == 1) return head;

        ListNode dummy(0);
        dummy.next = head;
        ListNode* prevGroupEnd = &dummy;

        while (true) {
            ListNode* groupEnd = prevGroupEnd;
            for (int i = 0; i < k; ++i) {
                groupEnd = groupEnd->next;
                if (!groupEnd) return dummy.next;
            }

            ListNode* groupStart = prevGroupEnd->next;
            ListNode* nextGroupStart = groupEnd->next;

            ListNode* prev = nextGroupStart;
            ListNode* curr = groupStart;
            while (curr != nextGroupStart) {
                ListNode* temp = curr->next;
                curr->next = prev;
                prev = curr;
                curr = temp;
            }

            prevGroupEnd->next = groupEnd;
            prevGroupEnd = groupStart;
        }
    }
};
```

## Explanation of Key Functions

### `reverseKGroup(ListNode* head, int k)`
This function reverses the nodes of the linked list in groups of size `k`:
1. **Group Identification**: Uses a pointer to find the end of each group of size `k`.
2. **Group Reversal**: Reverses the nodes within the identified group while linking it to the previous and next groups.
3. **Edge Cases**: If the number of nodes is not a multiple of `k`, the remaining nodes are left unchanged.

## Example Usage

### Input
- Linked List: `[1, 2, 3, 4, 5]`
- `k = 2`

### Output
- Reversed Linked List: `[2, 1, 4, 3, 5]`

### Input
- Linked List: `[1, 2, 3, 4, 5]`
- `k = 3`

### Output
- Reversed Linked List: `[3, 2, 1, 4, 5]`

## Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes in the linked list. Each node is processed once.
- **Space Complexity**: \(O(1)\), as the algorithm uses only a constant amount of extra space.

## Edge Cases Considered
- **List Size < k**: Returns the list as-is without any reversal.
- **List Size Not a Multiple of k**: Reverses complete groups and leaves the remaining nodes untouched.
- **Single Node List**: Returns the same list, as there are no groups to reverse.
- **`k = 1`**: Returns the same list, as reversing groups of size 1 has no effect.

## Summary
This program provides an efficient, in-place solution for reversing nodes in groups of size `k` within a singly linked list. By handling all common edge cases and ensuring optimal performance, it is a reliable approach to this problem.
