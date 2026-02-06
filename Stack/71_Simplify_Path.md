# LeetCode 71 - Simplify Path

---

## 📌 Problem

Given a string `path`, which is an absolute path in a Unix-style file system,  
convert it to the simplified canonical path.

Rules:

- `"."` → current directory (ignore)
- `".."` → go back one directory
- Multiple slashes `//` → treated as single `/`
- Result must:
  - Start with `/`
  - Have no trailing `/` (except root)

---

## 🧩 Example

Input:
```
"/home/"
```

Output:
```
"/home"
```

---

Input:
```
"/../"
```

Output:
```
"/"
```

---

Input:
```
"/home//foo/"
```

Output:
```
"/home/foo"
```

---

# 🚀 Approach (Stack)

## 🔑 Key Idea

- Split the path by `/`
- Use a stack to simulate directory navigation
- Process each part:

| Case | Action |
|------|--------|
| `""` or `"."` | Ignore |
| `".."` | Pop from stack (go back) |
| Directory name | Push to stack |

Finally, rebuild path from stack.

---

# 💻 Java Code

```java
class Solution {
    public String simplifyPath(String path) {

        String[] parts = path.split("/");
        Stack<String> st = new Stack<>();

        for (String p : parts) {
            if (p.equals("") || p.equals(".")) {
                continue;
            } 
            else if (p.equals("..")) {
                if (!st.isEmpty())
                    st.pop(); 
            } 
            else {
                st.push(p);
            }
        }

        StringBuilder sb = new StringBuilder();

        for (String dir : st) {
            sb.append("/").append(dir);
        }

        return sb.length() == 0 ? "/" : sb.toString();
    }
}
```

---

# 🎨 Graphical Representation

Example:

```
path = "/a/./b/../../c/"
```

---

### Step 1 → Split

```
["", "a", ".", "b", "..", "..", "c", ""]
```

---

### Step 2 → Process Using Stack

Start with empty stack:

```
[]
```

Read `"a"` → push

```
["a"]
```

Read `"."` → ignore

Read `"b"` → push

```
["a", "b"]
```

Read `".."` → pop

```
["a"]
```

Read `".."` → pop

```
[]
```

Read `"c"` → push

```
["c"]
```

---

### Step 3 → Build Final Path

```
"/c"
```

---

# 🎉 Final Answer

```
"/c"
```

---

# ⏱ Time Complexity

O(n)

- Split takes O(n)
- Stack operations are O(n)

---

# 📦 Space Complexity

O(n)

- Stack stores directory names

---

# 🧠 Why This Works

Stack simulates real file system navigation:

- Push → go into directory
- Pop → go back
- Ignore `"."`
- Ignore extra `/`

This guarantees canonical path.

---

# 🔥 Pattern Used

Stack  
String Processing  
Simulation  

---

# ⚡ Interview Insight

If interviewer asks:

Why not use recursion?

Because directory traversal is sequential and stack perfectly models navigation history.

---

# ✅ Final Output

Input:
```
"/a/./b/../../c/"
```

Output:
```
"/c"
```

