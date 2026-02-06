# LeetCode 1209 - Remove All Adjacent Duplicates in String II

---

## 📌 Problem

Given a string `s` and an integer `k`,  
remove all adjacent duplicates in the string where exactly `k` equal characters appear consecutively.

Return the final string after all such removals.

---

## 🧩 Example

Input:
```
s = "deeedbbcccbdaa"
k = 3
```

Output:
```
"aa"
```

Explanation:

```
deeedbbcccbdaa
→ dddbbcccbdaa     (remove eee)
→ dd bbb daa       (remove ccc)
→ dd daa           (remove bbb)
→ aa               (remove ddd)
```

---

# 🚀 Approach (Stack with Frequency)

## 🔑 Key Idea

Instead of storing just characters,  
we store:

```
[character, frequency]
```

So stack stores pairs like:

```
[a, 1]
[b, 2]
```

When frequency reaches `k`,  
we remove that group immediately.

---

# 💻 Java Code

```java
class Solution {
    public String removeDuplicates(String s, int k) {

        Stack<int[]> st = new Stack<>();

        for (char ch : s.toCharArray()) {

            if (!st.isEmpty() && st.peek()[0] == ch) {
                st.peek()[1]++;

                if (st.peek()[1] == k) {
                    st.pop();
                }
            } else {
                st.push(new int[] { ch, 1 });
            }
        }

        StringBuilder sb = new StringBuilder();

        for (int i = 0; i < st.size(); i++) {

            int[] pair = st.get(i);
            char ch = (char) pair[0];
            int count = pair[1];

            for (int j = 0; j < count; j++) {
                sb.append(ch);
            }
        }

        return sb.toString();
    }
}
```

---

# 🎨 Graphical Dry Run

Example:

```
s = "deeedbbcccbdaa"
k = 3
```

---

### Step 1

Read 'd'
```
[d,1]
```

Read 'e'
```
[d,1], [e,1]
```

Read 'e'
```
[d,1], [e,2]
```

Read 'e'
```
[d,1], [e,3]
```

Frequency == k → remove e group

```
[d,1]
```

---

Continue...

Eventually stack becomes:

```
[a,2]
```

Final string:
```
"aa"
```

---

# ⏱ Time Complexity

O(n)

- Each character pushed once.
- Each character popped at most once.

---

# 📦 Space Complexity

O(n)

- Stack may store entire string in worst case.

---

# 🧠 Why This Works

- We maintain compressed representation of string.
- As soon as count reaches `k`, we remove immediately.
- This automatically handles cascading deletions.

Example:
```
aaabbbccc
```
Removals happen naturally during traversal.

---

# 🔥 Pattern Used

Stack  
Frequency Counting  
Adjacent Removal  
Simulation  

---

# ⚡ Interview Optimization

Instead of `Stack<int[]>`,
you can use:

```
StringBuilder + int[] count array
```

That reduces object overhead and is slightly faster.

---

# ✅ Final Output

Input:
```
"deeedbbcccbdaa", k = 3
```

Output:
```
"aa"
```

---

# 🏆 Pattern Category

Stack with Count  
Advanced Adjacent Duplicate Removal  


