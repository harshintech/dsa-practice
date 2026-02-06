# LeetCode 739 - Daily Temperatures

---

## 📌 Problem

Given an array `temperatures`,  
return an array `res` such that:

- `res[i]` = number of days you have to wait after day `i`
  to get a warmer temperature.
- If there is no future warmer day → `0`.

---

## 🧩 Example

Input:
```
temperatures = [73,74,75,71,69,72,76,73]
```

Output:
```
[1,1,4,2,1,1,0,0]
```

---

# 🚀 Approach (Monotonic Stack)

## 🔑 Key Idea

We need the **next greater temperature on the right**.

So we use a:

👉 **Monotonic Decreasing Stack**

The stack stores **indices**, not values.

Why indices?

Because we need:
```
difference = future_index - current_index
```

---

# 💻 Java Code

```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {

        int[] res = new int[temperatures.length];
        Deque<Integer> st = new ArrayDeque<>();

        for (int i = 0; i < temperatures.length; i++) {

            while (!st.isEmpty() && temperatures[st.peek()] < temperatures[i]) {
                res[st.peek()] = i - st.pop();
            }

            st.push(i);
        }

        return res;
    }
}
```

---

# 🎨 Graphical Representation

Example:

```
[73,74,75,71,69,72,76,73]
```

---

### Step 1

Index 0 → 73

Stack:
```
[0]
```

---

### Step 2

Index 1 → 74

74 > 73 → pop 0

res[0] = 1 - 0 = 1

Stack:
```
[1]
```

---

### Step 3

Index 2 → 75

75 > 74 → pop 1

res[1] = 2 - 1 = 1

Stack:
```
[2]
```

---

### Step 4

Index 3 → 71

71 < 75 → push

Stack:
```
[2,3]
```

---

### Step 5

Index 4 → 69

69 < 71 → push

Stack:
```
[2,3,4]
```

---

### Step 6

Index 5 → 72

72 > 69 → pop 4 → res[4] = 1  
72 > 71 → pop 3 → res[3] = 2  

Stack:
```
[2,5]
```

---

### Step 7

Index 6 → 76

76 > 72 → pop 5 → res[5] = 1  
76 > 75 → pop 2 → res[2] = 4  

Stack:
```
[6]
```

---

### Step 8

Index 7 → 73

73 < 76 → push

Stack:
```
[6,7]
```

---

Final Result:

```
[1,1,4,2,1,1,0,0]
```

---

# ⏱ Time Complexity

O(n)

- Each element pushed once
- Each element popped once

---

# 📦 Space Complexity

O(n)

- Stack stores indices

---

# 🧠 Why Use Deque Instead of Stack?

Instead of:

```
Stack<Integer> st = new Stack<>();
```

We use:

```
Deque<Integer> st = new ArrayDeque<>();
```

### Reasons:

| Stack | Deque (ArrayDeque) |
|-------|-------------------|
| Old legacy class | Modern replacement |
| Synchronized (slower) | Faster |
| Rarely used now | Industry standard |

Both behave same (LIFO),  
but `ArrayDeque` is preferred in interviews & production.

---

# 🔥 Pattern Used

Monotonic Stack  
Next Greater Element  
Stack of Indices  

---

# ⚡ Interview Insight

Why store indices instead of values?

Because we need:

```
i - previousIndex
```

to calculate waiting days.

---

# ✅ Final Output

Input:
```
[73,74,75,71,69,72,76,73]
```

Output:
```
[1,1,4,2,1,1,0,0]
```
![itachiuchiha.png](https://assets.leetcode.com/users/images/7be18ad0-42f5-4844-88f5-d20ec55a0c1a_1770361981.9491723.png)

