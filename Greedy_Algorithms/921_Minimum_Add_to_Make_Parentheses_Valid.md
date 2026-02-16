# 🧩 Minimum Add to Make Parentheses Valid

---

## 📌 Problem

Given a string `s` consisting of only:

```
'(' and ')'
```

Return the **minimum number of parentheses** you must add to make it valid.

A valid string means:

- Every '(' has a matching ')'
- Every ')' has a matching '('

---

## 🧩 Example 1

Input:
```
s = "())"
```

Output:
```
1
```

We need one extra `'('` at the beginning or one `')'` at the end.

---

## 🧩 Example 2

Input:
```
s = "((("
```

Output:
```
3
```

We need 3 closing brackets.

---

# 🚀 Approach (Greedy Counting)

---

## 🔑 Core Idea

We track:

- `openCount` → unmatched '('
- `closeCount` → unmatched ')'

---

### 🔹 If we see '('

```
openCount++
```

---

### 🔹 If we see ')'

- If we have unmatched '(' → match it  
  ```
  openCount--
  ```
- Else → it's an extra ')'
  ```
  closeCount++
  ```

---

At the end:

```
Total needed = openCount + closeCount
```

---

# 💻 Java Code

```java
class Solution {
    public int minAddToMakeValid(String s) {

        int openCount = 0;
        int closeCount = 0;

        for(char ch : s.toCharArray()){

           if(ch == '(') {
               openCount++;
           } else {
               if(openCount > 0)
                   openCount--;
               else
                   closeCount++;
           }
        }

        return openCount + closeCount;
    }
}
```

---

# 🧠 Dry Run

Input:
```
"())("
```

Process:

```
'(' → open = 1
')' → open = 0
')' → close = 1
'(' → open = 1
```

Final:

```
open = 1
close = 1
```

Answer:
```
2
```

---

# ⏱ Time Complexity

```
O(n)
```

Single pass.

---

# 📦 Space Complexity

```
O(1)
```

Only counters used.

---

# 🔥 Why This Works

We are simply counting:

- Extra '(' that need ')'
- Extra ')' that need '('

No need for stack.

---

# 🏆 Pattern Used

Greedy  
Counter Tracking  
Parentheses Balancing  

---

# 🧠 Interview Insight

If problem asks:

- Minimum insertions
- Minimum additions
- Valid parentheses correction

Think:

```
Counter method (if only one bracket type)
Stack method (if multiple types)
```

---

# ✅ Final Output

Input:
```
"())("
```

Output:
```
2
```

---



