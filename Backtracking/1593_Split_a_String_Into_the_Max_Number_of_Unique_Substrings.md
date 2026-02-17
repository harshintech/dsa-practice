# 🔥 Maximum Unique Split (Backtracking)

---

## 📌 Problem

Given a string `s`, split it into the **maximum number of unique substrings**.

Rules:

- Every substring must be unique.
- You can split anywhere.
- Return the maximum count.

---

## 🧩 Example

Input:
```
s = "ababccc"
```

Output:
```
5
```

One valid split:
```
"a" | "b" | "ab" | "c" | "cc"
```

---

# 🚀 Approach (Backtracking + HashSet)

---

## 🔑 Core Idea

At each index:

Try every possible substring starting from that index.

If substring is not already used:

1️⃣ Add it to set  
2️⃣ Recurse  
3️⃣ Remove it (Backtrack)

Keep track of maximum splits.

---

# 💻 Java Code

```java
class Solution {
    public int maxUniqueSplit(String s) {
        return backtrack(0, s, new HashSet<>());
    }

    private int backtrack(int start, String s,HashSet<String> seen){

        if(start == s.length()){
            return 0;
        }

        int maxSplits = 0;

        for(int end = start + 1; end <= s.length(); end++){
            String substring = s.substring(start, end);
            if(!seen.contains(substring)){
                seen.add(substring);
                maxSplits = Math.max(maxSplits,1 + backtrack(end,s,seen));
                seen.remove(substring); // backtrack
            }
        }

        return maxSplits;
    }
}
```

---

# 🌳 Detailed Dry Run

Input:
```
"ababccc"
```

Length = 7

Call:
```
backtrack(0, {})
```

---

# 🌟 Maximum Path

---

### Step 1

Take:
```
"a"
```

```
seen = {a}
```

---

### Step 2

Take:
```
"b"
```

```
seen = {a, b}
```

---

### Step 3

Try:
```
"a" ❌ (already used)
"ab" ✅
```

```
seen = {a, b, ab}
```

---

### Step 4

Remaining:
```
"ccc"
```

Take:
```
"c"
```

```
seen = {a, b, ab, c}
```

---

### Step 5

Try:
```
"c" ❌
"cc" ✅
```

```
seen = {a, b, ab, c, cc}
```

---

### Step 6 (Base Case)

```
start == length
return 0
```

Unwinding:

```
Step 5 → 1
Step 4 → 2
Step 3 → 3
Step 2 → 4
Step 1 → 5
```

---

# 🎯 Final Answer

```
5
```

---

# ❓ Why Not More Than 5?

Try:
```
"a" | "b" | "a" ❌ duplicate
```

Try:
```
"ab" | "a" | "b" ❌ duplicate
```

Try:
```
"a" | "ba" | "b" | "c" | "c" ❌ duplicate
```

So maximum = 5.

---

# 🌳 Recursion Structure

```
(0,{})
 ├── "a"
 │     ├── "b"
 │     │     ├── "ab"
 │     │     │     ├── "c"
 │     │     │     │     ├── "cc" → 5 ✅
 │     │     │     │     └── "ccc" → 4
 │     │     └── smaller paths
 └── "ab"
       └── smaller paths
```

---

# ⏱ Time Complexity

Worst case:

```
O(n × 2^n)
```

Because each position can branch.

---

# 📦 Space Complexity

```
O(n)
```

For recursion + HashSet.

---

# 🔥 Pattern Used

Backtracking  
Set for uniqueness  
Partitioning string  

---

# 🧠 Interview Insight

Whenever problem says:

```
Split string
Maximize something
Ensure uniqueness
```

Think:

```
Backtracking + HashSet
```

---

# 🏆 Advanced Insight

This is harder than:

- Subsets
- Palindrome Partitioning

Because:

We must enforce uniqueness dynamically.

---

# ✅ Final Result

Input:
```
"ababccc"
```

Output:
```
5
```

---


