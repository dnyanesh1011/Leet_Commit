# 71. Simplify Path 🚀

## Problem Description

You are given an absolute path for a Unix-style file system, which always begins with a slash `/`. Your task is to transform this absolute path into its simplified canonical path.

The rules of a Unix-style file system are as follows:

1. A single period `.` represents the current directory.
2. A double period `..` represents the previous/parent directory.
3. Multiple consecutive slashes such as `//` and `///` are treated as a single slash `/`.
4. Any sequence of periods that does not match the rules above should be treated as a valid directory or file name. For example, `...` and `....` are valid directory or file names.

The simplified canonical path should follow these rules:

- The path must start with a single slash `/`.
- Directories within the path must be separated by exactly one slash `/`.
- The path must not end with a slash `/`, unless it is the root directory.
- The path must not have any single or double periods (`.` and `..`) used to denote current or parent directories.

**Return the simplified canonical path.**

---

## Examples

### Example 1:
**Input**:
```plaintext
path = "/home/"
```
**Output**:
```plaintext
"/home"
```

**Explanation**:
The trailing slash should be removed.

---

### Example 2:
**Input**:
```plaintext
path = "/home//foo/"
```
**Output**:
```plaintext
"/home/foo"
```

**Explanation**:
Multiple consecutive slashes are replaced by a single one.

---

### Example 3:
**Input**:
```plaintext
path = "/home/user/Documents/../Pictures"
```
**Output**:
```plaintext
"/home/user/Pictures"
```

**Explanation**:
A double period `..` refers to the directory up a level (the parent directory).

---

### Example 4:
**Input**:
```plaintext
path = "/../"
```
**Output**:
```plaintext
"/"
```

**Explanation**:
Going one level up from the root directory is not possible.

---

### Example 5:
**Input**:
```plaintext
path = "/.../a/../b/c/../d/./"
```
**Output**:
```plaintext
"/.../b/d"
```

**Explanation**:
`...` is a valid name for a directory in this problem.

---

## Approach

### Key Insights

1. **Use a Stack**: 
   - A stack is useful to simulate the process of navigating through the file system by pushing directories and popping them when navigating to the parent directory (`..`).
   
2. **String Processing**: 
   - Split the input path based on the `/` separator. Each segment will either be a directory name, `.` (current directory), or `..` (parent directory).
   
3. **Handle Special Cases**:
   - Ignore `.` (current directory) and handle `..` (parent directory) by popping the top of the stack.
   - If the path is empty or consists of only slashes, treat it as the root directory `/`.

---

## Solution Steps

1. **Initialize a Stack**:
   - This stack will store the valid directory names.

2. **Process Each Segment**:
   - Split the path by `/` and process each part:
     - If the part is `.` or an empty string, skip it.
     - If the part is `..`, pop the stack if it's not empty.
     - Otherwise, push the directory name onto the stack.

3. **Construct the Final Path**:
   - After processing all segments, join the stack elements with `/`.
   - If the stack is empty, return `/` to indicate the root directory.

---

## Complexity Analysis

### Time Complexity
- **Splitting Path**: \(O(n)\), where \(n\) is the length of the input path string.
- **Stack Operations**: Each directory name is pushed and popped at most once, so the overall complexity is \(O(n)\).

**Overall Complexity**: \(O(n)\), where \(n\) is the length of the input path.

### Space Complexity
- **Stack Storage**: At most \(O(n)\) space is used to store the directory names in the stack.

**Overall Space Complexity**: \(O(n)\).

---

## Solution Code

```cpp
class Solution {
public:
    string simplifyPath(string path) {
        vector<string> stack;
        string result, dir;
        stringstream ss(path);

        while (getline(ss, dir, '/')) {
            if (dir == "" || dir == ".") {
                continue; // Skip empty or current directory
            } else if (dir == "..") {
                if (!stack.empty()) {
                    stack.pop_back(); // Move up to the parent directory
                }
            } else {
                stack.push_back(dir); // Add the directory to the stack
            }
        }

        for (const string& d : stack) {
            result += "/" + d;
        }

        return result.empty() ? "/" : result;
    }
};
```

---

## Example Walkthrough

### Input: `/home/user/Documents/../Pictures`

1. **Initial Path**: `/home/user/Documents/../Pictures`
2. **Processing Segments**:
   - `/home`: Push "home".
   - `/user`: Push "user".
   - `/Documents`: Push "Documents".
   - `/..`: Pop the last element ("Documents").
   - `/Pictures`: Push "Pictures".
3. **Final Simplified Path**: `/home/user/Pictures`

**Output**: `/home/user/Pictures`

---

## Edge Cases

1. **Single Directory**:
   - Input: `/home`
   - Output: `/home`

2. **Empty Path**:
   - Input: `/`
   - Output: `/`

3. **Multiple Consecutive Slashes**:
   - Input: `/home//foo///bar`
   - Output: `/home/foo/bar`

4. **Going Up Beyond Root**:
   - Input: `/../`
   - Output: `/`

