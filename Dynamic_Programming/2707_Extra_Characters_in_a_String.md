# 🧩 Minimum Extra Characters in a String

---

## 📌 Problem

Given:

```
String s
Dictionary[] words
```

Split the string using dictionary words such that:

✅ Minimum number of **extra characters** remain.

Return:

```
minimum extra characters
```

---

## 🧩 Example

Input:
```
s = "leetscode"
dictionary = ["leet","code","leetcode"]
```

Valid split:
```
leet | s | code
```

Extra characters:
```
"s"
```

Output:
```
1
```

---

# 🚀 Core Idea (DP from Right → Left)

---

## 🔑 Meaning of DP

```
dp[i] =
minimum extra characters
from index i → end
```

Final answer:

```
dp[0]
```

---

# 🧠 Two Choices at Every Index

At index `i`:

---

## ✅ Choice 1 — Treat character as EXTRA

Skip current character.

```
dp[i] = 1 + dp[i+1]
```

---

## ✅ Choice 2 — Match Dictionary Word

Try every substring:

```
s[i...j]
```

If exists in dictionary:

```
dp[i] = min(dp[i], dp[j+1])
```

---

# 💻 Java Code

```java
class Solution {
    public int minExtraChar(String s, String[] dictionary) {

        Set<String> set = new HashSet<>();

        for(String word : dictionary)
            set.add(word);

        int n = s.length();
        int[] dp = new int[n + 1];

        for(int i = n - 1; i >= 0; i--) {
            // assume current char extra
            dp[i] = 1 + dp[i + 1];

            for(int j = i; j < n; j++) {
                if(set.contains(s.substring(i, j + 1))) {
                    dp[i] = Math.min(dp[i], dp[j + 1]);
                }
            }
        }

        return dp[0];
    }
}
```

---

# 🌳 Dry Run

```
s = "leetscode"
```

---

Start from end:

```
dp[9] = 0
```

---

### i = 8 → 'e'

No match

```
dp[8] = 1
```

---

### i = 5 → "code"

Dictionary match ✅

```
dp[5] = dp[9] = 0
```

---

### i = 0 → "leet"

Match found ✅

```
dp[0] = dp[4]
```

Remaining extra only:

```
"s"
```

Final:
```
dp[0] = 1
```

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

# 🔥 Pattern Used

String DP  
Word Break Variant  
Backward DP  

---

# 🧠 Relation With Word Break

| Problem | Goal |
|---|---|
| Word Break | Possible or not |
| Word Break II | All sentences |
| ✅ Min Extra Char | Min leftover |

Same foundation ✅

---

# ⚠ Important Insight

We always assume:

```
character is extra first
```

Then try improving answer using dictionary.

This guarantees optimal solution.

---

# 🏆 Interview Trick

Whenever question says:

```
Minimize leftover / unmatched characters
```

Think:

```
Word Break + DP Minimization
```

---

# ✅ Final Output

Input:
```
"leetscode"
```

Output:
```
1
```

---

