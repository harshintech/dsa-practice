# 🧩 Word Break Problem (DP + Trie)

---

## 📌 Problem

Given:

```
String s
Dictionary wordDict
```

Return:

```
true  → if string can be segmented using dictionary words
false → otherwise
```

Each word can be reused multiple times.

---

## 🧩 Example

```
s = "ilikesamsung"

wordDict =
["i", "like", "sam", "samsung", "mobile"]
```

Valid split:

```
i | like | samsung
```

✅ Output:
```
true
```

---

# 🚀 Approach 1 — Dynamic Programming (Optimal)

---

## 🔑 Core Idea

Let:

```
dp[i] = true
```

Meaning:

```
Substring s[0 → i-1] can be formed
using dictionary words.
```

---

### Initialization

```
dp[0] = true
```

Empty string is always valid.

---

# 💻 DP Code

```java
class Solution {
    public boolean wordBreak(String s,List<String> wordDict) {

        Set<String> set = new HashSet<>(wordDict);

        boolean[] dp = new boolean[s.length() + 1];
        dp[0] = true;

        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && set.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[s.length()];
    }
}
```

---

# 🧠 Dry Run

```
s = "ilikesamsung"
```

Index mapping:

```
i l i k e s a m s u n g
0 1 2 3 4 5 6 7 8 9...
```

---

### Start

```
dp[0] = true
```

---

### i = 1

Check:
```
"i"
```

Exists ✅

```
dp[1] = true
```

---

### i = 5

Check:
```
"like"
```

Valid because:

```
dp[1] = true
```

```
dp[5] = true
```

---

### i = 13

Check:
```
"samsung"
```

Valid because:

```
dp[5] = true
```

```
dp[13] = true
```

---

Final:

```
dp[n] = true
```

✅ Word break possible.

---

# ⏱ Time Complexity

```
O(n²)
```

Substring checking dominates.

---

# 📦 Space Complexity

```
O(n)
```

DP array.

---

# 🔥 Approach 2 — Trie + Recursion

---

## 🧠 Idea

Instead of HashSet lookup:

- Store dictionary inside Trie
- Try prefix splits recursively

---

## Trie Structure

```java
static class Node {
    Node[] children = new Node[26];
    boolean eow;
}
```

---

## Steps

1️⃣ Insert all dictionary words into Trie  
2️⃣ Try splitting string  
3️⃣ If prefix exists in Trie → recurse remaining part  

---

### Recursive Logic

```
wordBreak("ilikesamsung")

→ "i" exists
→ wordBreak("likesamsung")

→ "like" exists
→ wordBreak("samsung")

→ "samsung" exists
→ true
```

---

# ⚠ DP vs Trie Comparison

| Method | Time | Interview Preference |
|------|------|----------------|
| DP + HashSet | ✅ Fast | ⭐⭐⭐⭐⭐ |
| Trie + Recursion | Medium | ⭐⭐⭐ |
| Pure Recursion | Slow | ❌ |

---

# 🧠 Pattern Recognition

If problem says:

```
Split string using dictionary
```

Think immediately:

```
Word Break DP
```

---

# 🏆 Related Problems

- Word Break II
- Concatenated Words
- Extra Characters in String
- Trie Prefix Matching

---

# 🔥 Key Insight

We are checking:

```
Can prefix be formed?
```

NOT:

```
How many ways?
```

(Boolean DP)

---

# ✅ Final Answer

```
"ilikesamsung" → true
```

---



