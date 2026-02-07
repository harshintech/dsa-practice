# LeetCode 1189 - Maximum Number of Balloons

---

## 📌 Problem

Given a string `text`, return the maximum number of times you can form the word:

```
"balloon"
```

Each character in `text` can only be used once.

---

## 🧩 Example

Input:
```
text = "nlaebolko"
```

Output:
```
1
```

---

Input:
```
text = "loonbalxballpoon"
```

Output:
```
2
```

---

# 🚀 Approach (Frequency Counting)

## 🔑 Key Idea

The word `"balloon"` contains:

```
b → 1 time
a → 1 time
l → 2 times
o → 2 times
n → 1 time
```

So:

- Count frequency of all characters in `text`.
- Divide count of `l` and `o` by 2.
- Return the minimum among required characters.

Because the limiting character determines how many full words can be formed.

---

# 💻 Java Code (Array Version – Optimal)

```java
class Solution {
    public int maxNumberOfBalloons(String text) {

        int[] count = new int[26];

        for (char ch : text.toCharArray()) {
            count[ch - 'a']++;
        }

        int b = count['b' - 'a'];
        int a = count['a' - 'a'];
        int l = count['l' - 'a'] / 2;
        int o = count['o' - 'a'] / 2;
        int n = count['n' - 'a'];

        return Math.min(b, 
               Math.min(a, 
               Math.min(l, 
               Math.min(o, n))));
    }
}
```

---

# 💻 Alternative (HashMap Version)

```java
class Solution {
    public int maxNumberOfBalloons(String text) {

        HashMap<Character, Integer> map = new HashMap<>();

        for (char ch : text.toCharArray()) {
            map.put(ch, map.getOrDefault(ch, 0) + 1);
        }

        int b = map.getOrDefault('b', 0);
        int a = map.getOrDefault('a', 0);
        int l = map.getOrDefault('l', 0) / 2;
        int o = map.getOrDefault('o', 0) / 2;
        int n = map.getOrDefault('n', 0);

        return Math.min(b, 
               Math.min(a, 
               Math.min(l, 
               Math.min(o, n))));
    }
}
```

---

# 🎨 Graphical Explanation

Example:

```
text = "loonbalxballpoon"
```

Character counts:

```
b → 2
a → 2
l → 4
o → 4
n → 2
```

Since:

```
l needs 2 per word → 4 / 2 = 2
o needs 2 per word → 4 / 2 = 2
```

Minimum among:
```
2, 2, 2, 2, 2
```

Answer:
```
2
```

---

# ⏱ Time Complexity

O(n)

- Single pass through string.

---

# 📦 Space Complexity

O(1)

- Only 26 characters stored.

---

# 🧠 Why This Works

We only care about letters in `"balloon"`.

The smallest available required character limits the number of complete words.

Example:

If you have:
```
b = 3
a = 3
l = 1
o = 5
n = 3
```

You can only form:
```
1 balloon
```

Because `l` is limiting.

---

# 🔥 Pattern Used

Frequency Counting  
Greedy (Minimum Limiting Factor)  
Character Counting  

---

# ⚡ Interview Insight

Why divide `l` and `o` by 2?

Because `"balloon"` contains:

```
l → 2 times
o → 2 times
```

So we must account for that requirement.

---

# ✅ Final Output

Input:
```
"loonbalxballpoon"
```

Output:
```
2
```

---

# 🏆 Best Practice

Use array version instead of HashMap:

✔ Faster  
✔ Cleaner  
✔ Constant space  
✔ Preferred in interviews  


