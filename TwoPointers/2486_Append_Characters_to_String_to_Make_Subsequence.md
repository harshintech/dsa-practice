# LeetCode 2486 - 🧠 Append Characters to String to Make Subsequence

---

## 📌 Problem

Given two strings `s` and `t`.

Return the **minimum number of characters** that need to be appended to the end of `s` so that `t` becomes a subsequence of `s`.

---

## 🧩 Example

Input:
```
s = "coaching"
t = "coding"
```

Output:
```
4
```

---

## 🚀 Approach (Two Pointer Technique)

We try to match characters of `t` inside `s`.

### Idea:

- Use two pointers:
  - `sIdx` → iterate over `s`
  - `tIdx` → iterate over `t`
- Whenever characters match:
  - Move `tIdx`
- Always move `sIdx`
- At the end:
  - Remaining unmatched characters in `t`
  - = `t.length() - tIdx`

That is the answer.

---

## 💻 Java Code

```java
class Solution {
    public int appendCharacters(String s, String t) {

        int sIdx = 0;
        int sLen = s.length();

        int tIdx = 0;
        int tLen = t.length();

        while (sIdx < sLen && tIdx < tLen) {
            if (s.charAt(sIdx) == t.charAt(tIdx)) {
                tIdx++;
            }
            sIdx++;
        }

        return tLen - tIdx;
    }
}
```

---

## 🎨 Graphical Representation

Example:

```
s = coaching
t = coding
```

Step-by-step matching:

```
c o a c h i n g
↑
c o d i n g
↑
```

Match 'c' → move t pointer

```
c o a c h i n g
  ↑
  o d i n g
  ↑
```

Match 'o' → move t pointer

```
c o a c h i n g
      ↑
      d i n g
```

No 'd' found after scanning fully.

So unmatched part of `t`:
```
d i n g
```

Length = 4

Answer = 4

---

## ⏱ Time Complexity

O(n)

- We scan string `s` once.

---

## 📦 Space Complexity

O(1)

- Only pointers used.

---

## 🧠 Why This Works

- We are checking how much of `t` is already a subsequence of `s`.
- The remaining characters are the ones we must append.
- Greedy matching ensures maximum subsequence coverage.

---

## ✅ Final Formula

Answer = `t.length() - matched_characters`


