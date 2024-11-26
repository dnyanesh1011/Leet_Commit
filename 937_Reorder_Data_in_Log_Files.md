# 📜 Reorder Log Files

## Problem Statement

You are given an array of logs, where each log is a space-delimited string of words. The first word in each log is an identifier.

There are two types of logs:
1. **📄 Letter-logs**: All words (except the identifier) consist of lowercase English letters.
2. **🔢 Digit-logs**: All words (except the identifier) consist of digits.

You need to reorder the logs with the following rules:
1. The letter-logs come before all digit-logs.
2. The letter-logs are sorted lexicographically by their contents. If their contents are identical, then sort by their identifiers.
3. The digit-logs maintain their relative order.

---

## Examples

### Example 1:
**Input:**  
`logs = ["dig1 8 1 5 1","let1 art can","dig2 3 6","let2 own kit dig","let3 art zero"]`  
**Output:**  
`["let1 art can","let3 art zero","let2 own kit dig","dig1 8 1 5 1","dig2 3 6"]`

### Example 2:
**Input:**  
`logs = ["a1 9 2 3 1","g1 act car","zo4 4 7","ab1 off key dog","a8 act zoo"]`  
**Output:**  
`["g1 act car","a8 act zoo","ab1 off key dog","a1 9 2 3 1","zo4 4 7"]`

---

## Approach and Solution

The solution involves:
1. **Custom Sorting**: Implement a custom comparator to handle the sorting of letter-logs and digit-logs according to the rules.
   - Identify whether a log is a letter-log or a digit-log by checking the first character after the identifier.
   - If both logs are letter-logs, compare their contents lexicographically and, if necessary, their identifiers.
   - Ensure digit-logs maintain their relative order.

2. **Stable Sort**: Use `stable_sort` to maintain the relative order of digit-logs.

---

## Solution Code

```cpp
class Solution {
public:
    vector<string> reorderLogFiles(vector<string>& logs) {
        auto logComparator = [](const string& log1, const string& log2) {
            int index1 = log1.find(' ');
            string id1 = log1.substr(0, index1);
            string content1 = log1.substr(index1 + 1);

            int index2 = log2.find(' ');
            string id2 = log2.substr(0, index2);
            string content2 = log2.substr(index2 + 1);

            bool isDigit1 = isdigit(content1[0]);
            bool isDigit2 = isdigit(content2[0]);

            // Compare letter-logs
            if (!isDigit1 && !isDigit2) {
                if (content1 != content2) {
                    return content1 < content2;
                }
                return id1 < id2;
            }

            // Letter-logs come before digit-logs
            if (!isDigit1 && isDigit2) return true;
            if (isDigit1 && !isDigit2) return false;

            // Digit-logs maintain relative order
            return false;
        };

        stable_sort(logs.begin(), logs.end(), logComparator);
        return logs;
    }
};
```

---

## Complexity Analysis

### Time Complexity:
- **Sorting**: Sorting the logs involves a time complexity of **O(n log n)**, where `n` is the number of logs.
- **Comparison**: Each comparison involves extracting and comparing parts of the logs, which takes **O(L)** for a log of average length `L`.

Overall time complexity: **O(n log n * L)**.

### Space Complexity:
- The sorting process requires **O(log n)** additional space for the recursion stack.

---

## Key Insights

1. **Handling Letter-logs and Digit-logs**: Using a custom comparator allows us to distinguish between letter-logs and digit-logs efficiently.
2. **Stable Sorting**: Ensures that the digit-logs retain their relative order.

---

## Examples to Test

1. Logs with mixed letter-logs and digit-logs:
   - Input: `["dig1 8 2 3", "let2 art can", "let3 zoo", "dig2 4 5"]`
   - Output: `["let2 art can", "let3 zoo", "dig1 8 2 3", "dig2 4 5"]`

2. Logs with identical contents but different identifiers:
   - Input: `["let1 abc", "let2 abc"]`
   - Output: `["let1 abc", "let2 abc"]`

3. Logs with only digit-logs:
   - Input: `["dig1 8 1 5 1", "dig2 3 6"]`
   - Output: `["dig1 8 1 5 1", "dig2 3 6"]`

---

## Conclusion

The solution efficiently reorders the logs using a custom comparator and stable sort, meeting the problem's requirements. By leveraging lexicographical comparisons and separating letter-logs from digit-logs, the approach ensures correctness and clarity.
