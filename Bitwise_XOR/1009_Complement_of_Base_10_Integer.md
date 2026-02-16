# 🔁 Bitwise Complement of a Number

---

## 📌 Problem

Given a non-negative integer `n`,  
return its **bitwise complement**.

⚠ Only consider bits up to the highest set bit (ignore leading zeros).

---

## 🧩 Example

Input:
```
n = 5
```

Binary:
```
5 = 101
```

Complement:
```
010 = 2
```

Output:
```
2
```

---

# 🧠 Why We Need a Mask?

If we directly do:

```
~5
```

We get:

```
~5 = ....11111010
```

Because integers are stored in 32 bits (two's complement).

We only want to flip **relevant bits**.

So we create a **mask**.

---

# 🎯 Step-by-Step Logic

---

## 🔑 Step 1: Handle Edge Case

```java
if(n == 0) return 1;
```

Because:

```
0 → binary = 0
Complement = 1
```

---

## 🔑 Step 2: Build Mask

We build a mask of all 1's equal to the number of bits in `n`.

Example:

```
n = 5 → 101 (3 bits)
mask = 111
```

Code:

```java
while(temp > 0){
    mask = (mask << 1) | 1;
    temp = temp >> 1;
}
```

How it works:

Start:
```
mask = 0
```

Iteration 1:
```
mask = (0 << 1) | 1 = 1
```

Iteration 2:
```
mask = (1 << 1) | 1 = 11 (binary)
```

Iteration 3:
```
mask = (11 << 1) | 1 = 111
```

Done.

---

## 🔑 Step 3: Apply Complement Properly

```java
(~n) & mask
```

Example:

```
n = 5 = 101
~n = 11111010
mask = 00000111
----------------
Result = 00000010 = 2
```

---

# 💻 Java Code

```java
class Solution {
    public int bitwiseComplement(int n) {

        if(n == 0)
            return 1;

        int mask = 0;
        int temp = n;

        while(temp > 0){
            mask = (mask << 1) | 1;
            temp = temp >> 1;
        }

        return (~n) & mask;
    }
}
```

---

# ⏱ Time Complexity

Number of bits in n:

```
O(log n)
```

---

# 📦 Space Complexity

```
O(1)
```

---

# 🔥 Why Mask Is Necessary?

Because:

```
~n flips all 32 bits
```

But we only want to flip:

```
Bits up to MSB of n
```

Mask keeps only valid bits.

---

# 🧠 Bitwise Insight

| Operation | Meaning |
|------------|---------|
| `~` | Flip bits |
| `<<` | Left shift |
| `>>` | Right shift |
| `|` | OR |
| `&` | AND |

---

# 🏆 Alternative Trick (Optional)

You can also do:

```java
int mask = (1 << (Integer.toBinaryString(n).length())) - 1;
```

Then:

```java
return mask ^ n;
```

Because:

```
Complement = XOR with all 1's mask
```

---

# ✅ Final Example

Input:
```
n = 5
```

Output:
```
2
```

---


