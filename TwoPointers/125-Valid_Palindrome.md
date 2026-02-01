# LeetCode 125 – Valid Palindrome

## 🧠 Problem
Given a string `s`, determine if it is a palindrome, considering only **alphanumeric characters** and ignoring **case sensitivity**.

---

## 🧩 Pattern & Data Structure

- **Pattern:** Two Pointers (Left & Right)
- **Data Structure:** String

---

## 💡 Approach

1. Convert the string to lowercase.
2. Remove all non-alphanumeric characters.
3. Use two pointers:
   - `left` starts at the beginning
   - `right` starts at the end
4. Compare characters at both pointers.
   - If they differ, return `false`
   - Otherwise, move both pointers inward
5. If all characters match, return `true`.

---

## 🧮 Complexity Analysis

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(n)` (due to string normalization)

---

## ✅ Java Implementation

```java
class Solution {
    public boolean isPalindrome(String s) {

        s = s.toLowerCase().replaceAll("[^a-z0-9]", "");
        int left = 0;
        int right = s.length() - 1;

        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
}
