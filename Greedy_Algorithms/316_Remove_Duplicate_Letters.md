# 🧠 Remove Duplicate Letters (Monotonic Stack + Greedy)

---

## 📌 Problem

Given a string `s`, remove duplicate letters so that:

1️⃣ Every letter appears **once and only once**  
2️⃣ Result is **lexicographically smallest**

---

## 🧩 Example

Input:
```
s = "cbacdcbc"
```

Output:
```
"acdb"
```

---

# 🚀 Approach Overview

This problem uses:

```
Greedy + Monotonic Stack
```

---

## 🔑 Core Idea

For every character:

- If already used → skip
- While:
  - Stack top is bigger than current char
  - AND stack top appears again later
- Then:
  - Pop it (to make result lexicographically smaller)

---

# 💻 Java Code

```java
class Solution {
    public String removeDuplicateLetters(String s) {

        int[] lastIndex = new int[26];

        // Step 1: Store last occurrence of each char
        for(int i = 0; i < s.length(); i++){
            lastIndex[s.charAt(i) - 'a'] = i;
        }

        boolean[] seen = new boolean[26];
        Stack<Integer> st = new Stack<>();

        for(int i = 0; i < s.length(); i++){

            int curr = s.charAt(i) - 'a';

            if(seen[curr])
                continue;

            while(!st.isEmpty() &&
                  st.peek() > curr &&
                  i < lastIndex[st.peek()]){

                seen[st.pop()] = false;
            }

            st.push(curr);
            seen[curr] = true;
        }

        StringBuilder sb = new StringBuilder();

        while(!st.isEmpty()){
            sb.append((char)(st.pop() + 'a'));
        }

        return sb.reverse().toString();
    }
}
```

---

# 🧠 Why We Need `lastIndex`?

Because before popping a character, we must ensure:

```
It appears again later.
```

Otherwise, we would lose it permanently.

---

# 🔍 Example Trace

Input:
```
"cbacdcbc"
```

---

### Step 1: Build lastIndex

```
c → 7
b → 6
a → 2
d → 4
```

---

### Step-by-Step Execution

#### i = 0, 'c'
Stack empty → push

```
Stack: [c]
```

---

#### i = 1, 'b'

'b' < 'c'
Check: does 'c' appear later? Yes (index 7)

Pop 'c'

Push 'b'

```
Stack: [b]
```

---

#### i = 2, 'a'

'a' < 'b'
Check: 'b' appears later? Yes (index 6)

Pop 'b'

Push 'a'

```
Stack: [a]
```

---

#### i = 3, 'c'

Push 'c'

```
Stack: [a, c]
```

---

#### i = 4, 'd'

Push 'd'

```
Stack: [a, c, d]
```

---

#### i = 5, 'c'

Already seen → skip

---

#### i = 6, 'b'

'b' < 'd'
Check: does 'd' appear later?
No (lastIndex[d] = 4 < 6)

So we CANNOT pop 'd'

Push 'b'

```
Stack: [a, c, d, b]
```

---

#### i = 7, 'c'

Already seen → skip

---

# 🎯 Final Stack

```
[a, c, d, b]
```

Reverse →  

```
"acdb"
```

---

# ⏱ Time Complexity

Each element pushed & popped at most once:

```
O(n)
```

---

# 📦 Space Complexity

```
O(26) → constant
```

---

# 🔥 Pattern Used

Monotonic Stack  
Greedy  
Lexicographically Smallest Construction  

---

# 🧠 Important Condition Explained

```
while(!stack.isEmpty() &&
      stack.peek() > curr &&
      i < lastIndex[stack.peek()])
```

Means:

1️⃣ Top element is lexicographically bigger  
2️⃣ Current char is smaller  
3️⃣ Bigger char appears later  

So we remove bigger one now,  
because we can place it later.

---

# 🏆 Similar Problems

- Remove K Digits  
- Smallest Subsequence of Distinct Characters  
- Remove Adjacent Duplicates  

---

# ⚡ Interview Insight

This is a **classic monotonic stack problem**.

Whenever problem asks:

```
Smallest lexicographical string
while removing duplicates
```

Think:

```
Stack + Last Occurrence + Greedy
```

---

# ✅ Final Answer

Input:
```
"cbacdcbc"
```

Output:
```
"acdb"
```

---


