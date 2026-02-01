# LeetCode 151 -🔁 Reverse Words in a String 

## 🧠 Problem
Given a string `s`, reverse the order of words.  
A word is defined as a sequence of **non-space characters**.  
The returned string should have **only one space between words** and **no leading or trailing spaces**.

---

## 💡 Approach (Interview Explanation)

This solution follows a **String Processing** approach:

1. **Split the string** using `split(" +")`
   - `" +"` is a regex that matches **one or more spaces**
   - This safely handles:
     - Multiple spaces between words
     - Leading and trailing spaces

2. **Traverse words from end to start**
   - This reverses the word order

3. **Use `StringBuilder`**
   - Efficient for string concatenation in Java

4. **Trim the final result**
   - Removes the extra space added at the end

---

## ⏱️ Complexity Analysis
- Time Complexity: O(n)
- Space Complexity: O(n)

Where n is the length of the string.

---
## ✅ Java Solution

```java
class Solution {
    public String reverseWords(String s) {
        String[] word = s.split(" +");
        StringBuilder sb = new StringBuilder();

        for (int i = word.length - 1; i >= 0; i--) {
            sb.append(word[i]);
            sb.append(" ");
        }

        return sb.toString().trim();
    }
}
```



