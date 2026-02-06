# LeetCode 20 - Valid Parentheses

---

## 📌 Problem

Given a string `s` containing only the characters:

```
( ) { } [ ]
```

Return `true` if the input string is valid.

A string is valid if:

1. Open brackets must be closed by the same type.
2. Open brackets must be closed in the correct order.
3. Every closing bracket has a matching opening bracket.

---

## 🧩 Example

Input:
```
s = "()"
```
Output:
```
true
```

---

Input:
```
s = "()[]{}"
```
Output:
```
true
```

---

Input:
```
s = "(]"
```
Output:
```
false
```

---

# 🚀 Approach (Stack)

## 🔑 Key Idea

- Use a stack to store **opening brackets**.
- When a closing bracket appears:
  - Check if stack is empty → invalid.
  - Check if top matches corresponding opening bracket.
- At the end:
  - If stack is empty → valid.
  - Otherwise → invalid.

---

# 💻 Java Code

```java
class Solution {

    public char getParentheses(char ch) {
        if (ch == ')') ch = '(';
        if (ch == ']') ch = '[';
        if (ch == '}') ch = '{';

        return ch;
    }

    public boolean isValid(String s) {
        Stack<Character> st = new Stack<>();

        for(int i = 0; i < s.length(); i++){

            if(s.charAt(i) == '(' || 
               s.charAt(i) == '{' || 
               s.charAt(i) == '['){

                st.push(s.charAt(i));

            } else {

                if(st.isEmpty()) return false;

                char ch = getParentheses(s.charAt(i));

                if(st.peek() == ch){
                    st.pop();
                } else {
                    return false;
                }
            }
        }

        return st.isEmpty();
    }
}
```

---

# 🎨 Graphical Dry Run

Example:

```
s = "({[]})"
```

---

Start with empty stack:

```
[]
```

Read '(' → push
```
[(]
```

Read '{' → push
```
[(,{]
```

Read '[' → push
```
[(,{,[]
```

Read ']' → matches '[' → pop
```
[(,{]
```

Read '}' → matches '{' → pop
```
[(]
```

Read ')' → matches '(' → pop
```
[]
```

Stack empty → valid ✅

---

# ⏱ Time Complexity

O(n)

- Each character processed once.

---

# 📦 Space Complexity

O(n)

- Stack may hold all opening brackets.

---

# 🧠 Why This Works

Stack ensures:

- Last opened bracket must close first.
- Maintains correct nesting order.
- Detects mismatched or extra brackets instantly.

---

# 🔥 Pattern Used

Stack  
Parentheses Matching  
Balanced Brackets  

---

# ⚡ Interview Optimization

Instead of using `getParentheses()` method,
you can push expected closing bracket directly:

Example idea:

```
If '(' → push ')'
If '{' → push '}'
If '[' → push ']'
```

Then compare directly with current char.

This reduces extra function call.

---

# ✅ Final Output

Input:
```
"({[]})"
```

Output:
```
true"
```

