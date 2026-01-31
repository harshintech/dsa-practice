# LeetCode 28 – Find the Index of the First Occurrence in a String (strStr)

## 📌 Problem
Given two strings `haystack` and `needle`, return the index of the first occurrence of `needle` in `haystack`.  
If `needle` is not part of `haystack`, return `-1`.

---

## 🧠 Approach 1: Optimized Brute Force (Recommended)

### ✅ Idea
- Try every possible starting index in `haystack`
- Compare characters directly using `charAt`
- Avoid creating extra substrings (memory efficient)

### ⏱ Time Complexity
O(n × m)

### 📦 Space Complexity
O(1)

### 💻 Code

```java
class Solution {
    public int strStr(String haystack, String needle) {

        if (needle.length() == 0) return 0;

        for (int i = 0; i <= haystack.length() - needle.length(); i++) {

            int j = 0;

            while (j < needle.length() &&
                   haystack.charAt(i + j) == needle.charAt(j)) {
                j++;
            }

            if (j == needle.length()) {
                return i;
            }
        }

        return -1;
    }
}
```

## 🧠 Approach 2: Using substring()

### ⚠️ Note
-This method creates a new substring object at each iteration.
-It works but is less memory efficient.

### ⏱ Time Complexity
O(n × m)

### 💻 Code

```java
class Solution {
    public int strStr(String haystack, String needle) {

        if (haystack.length() < needle.length()) {
            return -1;
        }

        for (int i = 0; i <= haystack.length() - needle.length(); i++) {
            if (haystack.substring(i, i + needle.length()).equals(needle)) {
                return i;
            }
        }

        return -1;
    }
}
```

## 🧠 Approach 3: Pointer Based Brute Force

### ✅ Idea
-Use two pointers i and j
-Reset pointers on mismatch

### ⏱ Time Complexity
O(n × m)

### 💻 Code

```java
class Solution {
    public int strStr(String haystack, String needle) {

        if (haystack.length() < needle.length()) {
            return -1;
        }

        int i = 0;
        int j = 0;

        while (i < haystack.length()) {

            int index = i;

            while (i < haystack.length() && 
                   haystack.charAt(i) == needle.charAt(j)) {

                if (j == needle.length() - 1) {
                    return index;
                }

                i++;
                j++;
            }

            i = index + 1;
            j = 0;
        }

        return -1;
    }
}

```
