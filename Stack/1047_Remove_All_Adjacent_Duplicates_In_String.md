# LeetCode 1047 - Remove All Adjacent Duplicates In String

---

## 📌 Problem

Given a string `s`, repeatedly remove adjacent duplicate characters  
until no duplicates remain.

Return the final string.

---

## 🧩 Example

Input:
```
s = "abbaca"
```

Output:
```
"ca"
```

Explanation:

```
abbaca
→ aaca   (remove bb)
→ ca     (remove aa)
```

---

# 🚀 Approach 1: Stack

## 🔑 Idea

- Use stack to simulate removal.
- Traverse string:
  - If top of stack equals current char → pop.
  - Else → push.
- Build result from stack.

---

## 💻 Code (Stack Version)

```java
class Solution {
    public String removeDuplicates(String s) {

        Stack<Character> st = new Stack<>();

        for(int i = 0; i < s.length(); i++){

            if(!st.isEmpty() && st.peek() == s.charAt(i)){
                st.pop();
            } else {
                st.push(s.charAt(i));
            }
        }

        StringBuilder sb = new StringBuilder();
        while(!st.isEmpty()){
            sb.append(st.pop());
        }

        return sb.reverse().toString();
    }
}
```

---

## ⏱ Complexity

Time: O(n)  
Space: O(n)  

Each character pushed and popped at most once.

---

# 🚀 Approach 2: StringBuilder as Stack (Better)

## 🔑 Idea

Instead of `Stack`, use `StringBuilder`:

- Append character.
- If last character equals current → remove it.
- More efficient and cleaner.

---

## 💻 Code (Optimized Version)

```java
class Solution {
    public String removeDuplicates(String s) {

        StringBuilder stack = new StringBuilder();

        for (char c : s.toCharArray()) {
            int len = stack.length();

            if (len > 0 && stack.charAt(len - 1) == c) {
                stack.deleteCharAt(len - 1);
            } else {
                stack.append(c);
            }
        }

        return stack.toString();
    }
}
```

---

# 🎨 Graphical Dry Run

Example:
```
s = "abbaca"
```

Start with empty stack:

```
[]
```

Read 'a':
```
[a]
```

Read 'b':
```
[a,b]
```

Read 'b':
Top = b → duplicate → pop
```
[a]
```

Read 'a':
Top = a → duplicate → pop
```
[]
```

Read 'c':
```
[c]
```

Read 'a':
```
[c,a]
```

Final result:
```
"ca"
```

---

# 📊 Comparison

| Approach | Time | Space | Recommended |
|----------|------|-------|-------------|
| Stack | O(n) | O(n) | Good |
| StringBuilder | O(n) | O(n) | Best |

---

# 🧠 Why StringBuilder is Better?

✔ No stack object overhead  
✔ Faster in Java  
✔ Cleaner code  
✔ Industry-preferred  

---

# 🔥 Pattern Used

Stack  
Adjacent Removal  
Simulation  

---

# ✅ Final Output

Input:
```
"abbaca"
```

Output:
```
"ca"
```

---

# ⚡ Interview Tip

If interviewer asks:

Can we solve without stack?

Answer:

Yes, use `StringBuilder` as a stack for better performance.


