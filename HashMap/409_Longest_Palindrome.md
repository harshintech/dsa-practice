# LeetCode 409 - Longest Palindrome

---

## 📌 Problem

Given a string `s` consisting of uppercase and lowercase letters,  
return the length of the **longest palindrome** that can be built with those letters.

Letters are case-sensitive.

---

## 🧩 Example

Input:
```
"abccccdd"
```

Output:
```
7
```

Explanation:

We can build:
```
"dccaccd"
```

Length = 7

---

# 🚀 Approach (Frequency + Odd Count Tracking)

## 🔑 Key Idea

- A palindrome allows:
  - All characters with even frequency
  - Only **one** character with odd frequency (center)

So we:

1. Count character frequency.
2. Track how many characters have odd frequency.
3. If more than one odd exists:
   - Remove `(oddCount - 1)` characters.
4. Final formula:

If `oddCount > 1`:
```
return s.length() - oddCount + 1;
```
Else:
```
return s.length();
```

---

# 💻 Java Code (Your Smart Version)

```java
class Solution {
    public int longestPalindrome(String s) {

        Map<Character,Integer> map = new HashMap<>();

        int oddCount = 0;

        for(char ch : s.toCharArray()){
            map.put(ch, map.getOrDefault(ch, 0) + 1);

            if(map.get(ch) % 2 == 1){
                oddCount++;
            } else {
                oddCount--;
            }
        }

        if(oddCount > 1){
            return s.length() - oddCount + 1;
        }

        return s.length();
    }
}
```

---

# 🎨 Why This Works

Each time frequency changes:

| Previous | New | Effect |
|----------|-----|--------|
| Even | Odd | oddCount++ |
| Odd | Even | oddCount-- |

So `oddCount` always tracks number of characters with odd frequency.

---

# 🧠 Mathematical Insight

If:

```
oddCount = 3
```

We can use:

```
Only 1 odd fully.
Remaining 2 odd → lose 1 char each.
```

So total length becomes:

```
s.length() - (oddCount - 1)
```

Which simplifies to:

```
s.length() - oddCount + 1
```

---

# 🔎 Example Walkthrough

Input:
```
"abccccdd"
```

Counts:
```
a = 1 (odd)
b = 1 (odd)
c = 4 (even)
d = 2 (even)
```

oddCount = 2

Result:
```
8 - 2 + 1 = 7
```

---

# ⏱ Time Complexity

O(n)

- Single pass through string.

---

# 📦 Space Complexity

O(1)

- At most 128 ASCII characters stored.

---

# 🏆 Alternative (Array Version)

```java
class Solution {
    public int longestPalindrome(String s) {

        int[] freq = new int[128];

        for (char c : s.toCharArray()) {
            freq[c]++;
        }

        int length = 0;
        boolean hasOdd = false;

        for (int count : freq) {
            if (count % 2 == 0) {
                length += count;
            } else {
                length += count - 1;
                hasOdd = true;
            }
        }

        if (hasOdd) length++;

        return length;
    }
}
```

---

# 🔥 Pattern Used

Frequency Counting  
Greedy (Use All Even, Allow One Odd)  

---

# ✅ Final Output

Input:
```
"abccccdd"
```

Output:
```
7
```

---

# 🎯 Interview Insight

Only one character with odd frequency can sit in the center of a palindrome.

That is the core trick.

> “First make it work. Then make it right. Then make it fast.”




