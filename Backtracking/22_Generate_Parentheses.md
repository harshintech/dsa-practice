# Leetcode 22 - Generate Parentheses (Backtracking)

---

## 📌 Problem

Given `n` pairs of parentheses,  
generate all combinations of **well-formed parentheses**.

---

## 🧩 Example

Input:
```
n = 3
```

Output:
```
[
 "((()))",
 "(()())",
 "(())()",
 "()(())",
 "()()()"
]
```

---

# 🚀 Approach (Backtracking with Constraints)

---

## 🔑 Core Idea

At every step:

We can add:

```
"("  if left < n
")"  if right < left
```

This ensures:

- We never add more than `n` opening brackets.
- We never create invalid sequences.

---

# 💻 Java Code

```java
class Solution {

    public List<String> generateParenthesis(int n) {

        List<String> res = new ArrayList<>();

        recurse(res, 0, 0, "", n);

        return res;
    }

    public void recurse(List<String> res,
                        int left,
                        int right,
                        String s,
                        int n){

        // Base Case
        if(s.length() == n * 2){
            res.add(s);
            return;
        }

        // Add "(" if allowed
        if(left < n){
            recurse(res, left + 1, right,
                    s + "(", n);
        }

        // Add ")" if valid
        if(right < left){
            recurse(res, left, right + 1,
                    s + ")", n);
        }
    }
}
```

---

# 🧠 Why Conditions Work

### 1️⃣ `left < n`

We can only add `n` opening brackets.

---

### 2️⃣ `right < left`

We cannot close more brackets than opened.

This prevents invalid strings like:

```
")("
"())("
```

---

# 🌳 Recursion Tree (n = 3)

```
                                   (0,0,"")
                                        |
                                   (1,0,"(")
                                        |
                 -------------------------------------------------
                 |                                               |
          (2,0,"((")                                       (1,1,"()")
          /          \                                             |
 (3,0,"(((")     (2,1,"(()")                                 (2,1,"()(")
      |           /        \                                  /            \
(3,1,"((()") (3,1,"(()(") (2,2,"(())")               (3,1,"()((")   (2,2,"()()")
      |           |              |                           |              |
(3,2,"((())") (3,2,"(()()") (3,2,"(())(")           (3,2,"()(()")  (3,2,"()()(")
      |           |              |                           |              |
(3,3,"((()))") (3,3,"(()())") (3,3,"(())()")       (3,3,"()(())")  (3,3,"()()()")
      |           |              |                           |              |
     ADD         ADD            ADD                         ADD            ADD

```

Valid outputs:
```
((()))
(()())
(())()
()(())
()()()

```

---


# ⏱ Time Complexity

Total valid combinations:

```
Catalan Number
```

Approx:

```
O(4^n / √n)
```

---

# 📦 Space Complexity

Recursion depth:
```
O(n)
```

Result storage:
```
O(Catalan(n))
```

---

# 🔥 Pattern Used

Backtracking  
Constraint Checking  
Balanced Structure Generation  

---

# 🏆 Why This Is Important

This problem teaches:

- Pruning invalid branches early
- Constraint-based recursion
- Classic interview backtracking

---

# ⚠ Optimization Tip

Instead of:

```
String s + "("
```

You can use `StringBuilder` for better performance.

---

# ✅ Final Output

Input:
```
n = 3
```

Output:
```
5 valid combinations
```

---
