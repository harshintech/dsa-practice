# LeetCode 3 - Longest Substring Without Repeating Characters

---

## 📌 Problem

Given a string `s`, find the length of the longest substring without repeating characters.

---

## 🧩 Example

Input:
```
s = "abcabcbb"
```

Output:
```
3
```

Explanation:
The answer is `"abc"`.

---

Input:
```
s = "bbbbb"
```

Output:
```
1
```

---

# 🚀 Approach (Sliding Window + HashMap)

## 🔑 Key Idea

We need the **longest substring with all unique characters**.

So we:

- Use a sliding window.
- Expand window using `end`.
- If duplicate found → shrink window from `start`.
- Keep updating maximum length.

---

# 💡 Algorithm Steps

1. Create a `HashMap<Character, Integer>`
2. Use two pointers:
   - `start`
   - `end`
3. While `end < s.length()`:
   - If character already exists in map:
     - Remove characters from left until duplicate removed.
   - Update max length.
   - Add current character to map.
   - Move `end`

---

# 💻 Java Code

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {

        Map<Character,Integer> map = new HashMap<>();

        int start = 0;
        int end = 0;
        int maxLen = 0;

        while(end < s.length()){

            while(map.containsKey(s.charAt(end))){
                char left = s.charAt(start);
                map.remove(left);
                start++;
            }

            maxLen = Math.max(maxLen, end - start + 1);
            map.put(s.charAt(end), end);
            end++;
        }

        return maxLen;
    }
}
```

---

# 🎨 Graphical Representation

Example:

```
s = "abcabcbb"
```

---

### Step 1

```
[a]
maxLen = 1
```

---

### Step 2

```
[a b]
maxLen = 2
```

---

### Step 3

```
[a b c]
maxLen = 3
```

---

### Step 4 (duplicate 'a')

Window before:
```
[a b c] a
```

Remove from left until duplicate gone:

```
[b c] a
```

New window:
```
[b c a]
```

---

Continue sliding...

Final maximum window:

```
[a b c]
```

Length = 3

---

# ⏱ Time Complexity

O(n)

- Each character enters window once.
- Each character removed once.

---

# 📦 Space Complexity

O(min(n, 128))

- HashMap stores at most all unique characters.

---

# 🧠 Why This Works

Sliding window maintains:

- Always unique characters
- Expands greedily
- Shrinks only when invalid

This guarantees optimal solution.

---

# 🔥 Pattern Used

Sliding Window  
HashMap  
Longest Substring  
Two Pointers  

---

# ⚠ Important Optimization Note

A more optimal version can directly move `start` to:

```
start = max(start, map.get(currentChar) + 1)
```

That avoids removing one-by-one.

---

# ✅ Final Answer

Input:
```
"abcabcbb"
```

Output:
```
3
```

