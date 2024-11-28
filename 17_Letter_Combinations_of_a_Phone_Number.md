# 📞 Letter Combinations of a Phone Number  

## Problem Statement  

Given a string containing digits from **2-9** inclusive, return all possible letter combinations the number could represent. The mapping of digits to letters corresponds to the typical telephone keypad.  

The mapping is as follows:  
- **2 → "abc"**  
- **3 → "def"**  
- **4 → "ghi"**  
- **5 → "jkl"**  
- **6 → "mno"**  
- **7 → "pqrs"**  
- **8 → "tuv"**  
- **9 → "wxyz"**  

---

## Examples  

### Example 1  

**Input**:  
```plaintext  
digits = "23"  
```  
**Output**:  
```plaintext  
["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]  
```  

### Example 2  

**Input**:  
```plaintext  
digits = ""  
```  
**Output**:  
```plaintext  
[]  
```  

### Example 3  

**Input**:  
```plaintext  
digits = "2"  
```  
**Output**:  
```plaintext  
["a", "b", "c"]  
```  

---

## Approach  

### Backtracking  

1. **Key Idea**:  
   Use a backtracking algorithm to generate all possible combinations of letters for the given digits.  

2. **Steps**:  
   - Map each digit to its corresponding letters.  
   - Start with an empty combination and a pointer to the current digit.  
   - Append a letter from the current digit's mapping to the combination, then move to the next digit.  
   - Once all digits are processed, add the combination to the results.  

3. **Edge Cases**:  
   - If the input is an empty string, return an empty list.  
   - If the input contains only one digit, return the corresponding letters.  

---

## Solution Code  

```cpp  
class Solution {  
public:  
    vector<string> letterCombinations(string digits) {  
        if (digits.empty()) {  
            return {};  
        }  

        vector<string> digitToLetters = {  
            "", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"  
        };  
        vector<string> result;  
        string combination;  

        backtrack(0, digits, digitToLetters, combination, result);  
        return result;  
    }  

private:  
    void backtrack(int index, const string& digits, const vector<string>& digitToLetters,  
                   string& combination, vector<string>& result) {  
        if (index == digits.size()) {  
            result.push_back(combination);  
            return;  
        }  

        string letters = digitToLetters[digits[index] - '0'];  
        for (char letter : letters) {  
            combination.push_back(letter);  
            backtrack(index + 1, digits, digitToLetters, combination, result);  
            combination.pop_back();  
        }  
    }  
};  
```  

---

## Complexity Analysis  

### Time Complexity  
- The total number of combinations is proportional to \( 3^m \cdot 4^n \), where \(m\) and \(n\) are the number of digits that map to 3 and 4 letters, respectively.  

### Space Complexity  
- \(O(N)\): Space for the recursion stack, where \(N\) is the length of the input string.  

---

## Edge Cases  

1. **Empty Input**:  
   Input: `digits = ""`  
   Output: `[]`  

2. **Single Digit Input**:  
   Input: `digits = "7"`  
   Output: `["p", "q", "r", "s"]`  

3. **All Digits Mapping to 3 Letters**:  
   Input: `digits = "234"`  
   Output: Combinations with each digit mapped to 3 letters.  

4. **Combination of 3 and 4 Letter Digits**:  
   Input: `digits = "79"`  
   Output: Combinations with 4 letters for both digits.  

---

## Conclusion  

This solution effectively generates all combinations using backtracking, handling edge cases and ensuring optimal performance for typical input sizes.
