# LeetCode 402 - Remove K Digits

---

## 📌 Problem

Given a non-negative integer `num` represented as a string and an integer `k`,  
remove `k` digits from the number so that the new number is the smallest possible.

Return the result as a string.

---

## 🧩 Example

Input:
```
num = "1432219"
k = 3
```

Output:
```
"1219"
```

Explanation:
Remove digits `4`, `3`, and `2` → smallest number formed is `1219`.

---

Input:
```
num = "10200"
k = 1
```

Output:
```
"200"
```

---

Input:
```
num = "10"
k = 2
```

Output:
```
"0"
```

---

# 🚀 Approach (Monotonic Increasing Stack)

## 🔑 Key Idea

To get the smallest number:

- Remove larger digits that appear before smaller digits.
- Use a **monotonic increasing stack**.
- If current digit is smaller than stack top → pop.
- Continue until `k` removals done.

This greedily ensures the smallest possible number.

---

# 💻 Java Code

```java
class Solution {
    public String removeKdigits(String num, int k) {

        int len = num.length();

        if (len == k) {
            return "0";
        }

        Stack<Character> stack = new Stack<>();
        int i = 0;

        while (i < num.length()) {

            char curr = num.charAt(i);

            while (k > 0 && !stack.isEmpty() && stack.peek() > curr) {
                stack.pop();
                k--;
            }

            stack.push(curr);
            i++;
        }

        // If k still remains (example: 12345)
        while (k > 0) {
            stack.pop();
            k--;
        }

        StringBuilder sb = new StringBuilder();

        while (!stack.isEmpty()) {
            sb.append(stack.pop());
        }

        sb.reverse();

        // Remove leading zeros
        while (sb.length() > 1 && sb.charAt(0) == '0') {
            sb.deleteCharAt(0);
        }

        return sb.toString();
    }
}
```

---

# 🎨 Graphical Dry Run

Example:
```
num = "1432219"
k = 3
```

---

### Step-by-step

Start with empty stack:

```
[]
```

Read '1'
```
[1]
```

Read '4'
```
[1,4]
```

Read '3'

4 > 3 → pop 4 (k=2)

```
[1]
```

Push 3:
```
[1,3]
```

Read '2'

3 > 2 → pop 3 (k=1)

```
[1]
```

Push 2:
```
[1,2]
```

Read '2'
```
[1,2,2]
```

Read '1'

2 > 1 → pop 2 (k=0)

```
[1,2]
```

Push 1:
```
[1,2,1]
```

Continue pushing remaining digits.

Final stack:
```
[1,2,1,9]
```

Result:
```
"1219"
```

---

# ⏱ Time Complexity

O(n)

- Each digit pushed once.
- Each digit popped at most once.

---

# 📦 Space Complexity

O(n)

- Stack stores digits.

---

# 🧠 Why This Works

Greedy strategy:

If a bigger digit appears before a smaller digit,
removing the bigger one reduces the overall number more.

Monotonic increasing stack ensures:

Left side digits are always as small as possible.

---

# 🔥 Pattern Used

Monotonic Stack  
Greedy  
Digit Removal  
String Manipulation  

---

# ⚡ Important Edge Case

If digits are already increasing:

Example:
```
num = "12345", k = 2
```

No popping happens inside loop.

So we remove from the end:
```
→ "123"
```

---

# ✅ Final Output

Input:
```
"1432219", k = 3
```

Output:
```
"1219"
```

---

# 🏆 Interview Insight

If interviewer asks:

Why stack?

Because we need dynamic removal based on future smaller digits.

Without stack → brute force would be much harder.

