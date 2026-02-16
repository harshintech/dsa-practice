# 🔢 Largest Palindromic Number

---

## 📌 Problem

Given a string `num` representing digits:

Build the **largest palindromic number** using those digits.

Rules:

- Each digit can be used at most as many times as it appears.
- No leading zeros (unless answer is `"0"`).

---

## 🧩 Example

Input:
```
"444947137"
```

Output:
```
"7449447"
```

---

# 🚀 Approach (Greedy + Frequency Count)

---

## 🔑 Core Idea

To build the largest palindrome:

1️⃣ Build the **left half** using largest digits first  
2️⃣ Choose the **largest possible middle digit** (if any leftover)  
3️⃣ Mirror the left half to create the right half  

---

# 🧠 Why Greedy Works?

For maximum number:

```
Higher digits must appear first.
```

So we iterate:

```
9 → 0
```

---

# 💻 Java Code (Array Version – Optimal)

```java
class Solution {
    public String largestPalindromic(String num) {

        int[] freq = new int[10];

        // Count frequency
        for (char c : num.toCharArray()) {
            freq[c - '0']++;
        }

        StringBuilder left = new StringBuilder();

        // Build left half
        for (int i = 9; i >= 0; i--) {

            // Avoid leading zero
            if (i == 0 && left.length() == 0)
                break;

            while (freq[i] >= 2) {
                left.append(i);
                freq[i] -= 2;
            }
        }

        // Choose middle digit
        StringBuilder middle = new StringBuilder();
        for (int i = 9; i >= 0; i--) {
            if (freq[i] > 0) {
                middle.append(i);
                break;
            }
        }

        // Edge case: only zeros
        if (left.length() == 0 && middle.length() == 0)
            return "0";

        String right = new StringBuilder(left).reverse().toString();

        return left.toString() + middle + right;
    }
}
```

---

# 🧠 Step-by-Step Example

Input:
```
"444947137"
```

### Step 1: Frequency

```
4 → 4 times
7 → 2 times
9 → 1 time
3 → 1 time
1 → 1 time
```

---

### Step 2: Build Left Half

Start from 9:

- 9 → only 1 → save for middle
- 7 → 2 → add one pair → "7"
- 4 → 4 → add two pairs → "744"

Left:
```
"744"
```

---

### Step 3: Middle

Largest leftover digit:
```
9
```

---

### Step 4: Mirror

Right:
```
"447"
```

Final:
```
744 + 9 + 447
```

Output:
```
"7449447"
```

---

# ⚠ Important Condition

```
if (i == 0 && left.length() == 0)
```

Prevents leading zero.

Example:

Input:
```
"0000"
```

Without this check:
```
"0000"
```

Correct answer:
```
"0"
```

---

# ⏱ Time Complexity

Counting:
```
O(n)
```

Building:
```
O(10)
```

Total:
```
O(n)
```

---

# 📦 Space Complexity

```
O(10) → constant
```

---

# 🔥 Pattern Used

Greedy  
Frequency Counting  
Palindrome Construction  

---

# 🏆 Interview Insight

Whenever problem says:

```
Build largest / smallest palindrome from digits
```

Think:

1️⃣ Count frequency  
2️⃣ Build half  
3️⃣ Choose best middle  
4️⃣ Mirror  

---

# 🧠 Edge Cases

| Input | Output |
|--------|--------|
| "0000" | "0" |
| "00009" | "9" |
| "1" | "1" |

---

# ✅ Final Output

Input:
```
"444947137"
```

Output:
```
"7449447"
```

---


