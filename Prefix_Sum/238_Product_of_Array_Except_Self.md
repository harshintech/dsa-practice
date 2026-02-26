# 🔥 Product of Array Except Self

---

## 📌 Problem

Given an array:

```
nums = [a, b, c, d]
```

Return:

```
[
 product of all except a,
 product of all except b,
 product of all except c,
 product of all except d
]
```

⚠️ Without using division.

---

## ✅ Code

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {

        int n = nums.length;
        int pre[] = new int[n];
        int suff[] = new int[n];

        pre[0] = 1;
        suff[n-1] = 1;

        for(int i = 1;i < n;i++){
            pre[i] = pre[i - 1] * nums[i - 1];
        }

        for(int i = n - 2;i >= 0;i--){
            suff[i] = suff[i + 1] * nums[i + 1];
        }

        int ans[] = new int[n];
        for(int i =  0;i < n;i++){
            ans[i] = pre[i] * suff[i];
        }

        return ans;
    }
}
```

---

# 🧠 REAL LOGIC (MOST IMPORTANT)

For every index `i`:

```
Answer[i] =
(product of LEFT elements)
×
(product of RIGHT elements)
```

---

## 🎯 Key Observation

If we split array at index `i`:

```
LEFT SIDE        CURRENT        RIGHT SIDE
-------------------------------------------
nums[0..i-1]     nums[i]        nums[i+1..n-1]
```

We only need:

```
LEFT PRODUCT × RIGHT PRODUCT
```

---

# ✅ Step 1 — Prefix Product (`pre[]`)

```
pre[i] =
product of all elements BEFORE index i
```

Meaning:

```
pre[i] = nums[0] * nums[1] * ... * nums[i-1]
```

So:

```
pre[0] = 1
```

Because nothing exists on left.

---

### Example Meaning

```
nums = [2,3,4,5]

pre =
[1,
 2,
 2×3,
 2×3×4]
```

👉 Stores LEFT contribution.

---

# ✅ Step 2 — Suffix Product (`suff[]`)

```
suff[i] =
product of all elements AFTER index i
```

Meaning:

```
suff[i] = nums[i+1] * nums[i+2] * ...
```

So:

```
suff[n-1] = 1
```

Because nothing exists on right.

---

Example:

```
suff =
[3×4×5,
 4×5,
 5,
 1]
```

👉 Stores RIGHT contribution.

---

# ✅ Step 3 — Final Idea

Now for each index:

```
ans[i] = pre[i] * suff[i]
```

Why?

Because:

```
(pre[i])  → all left elements
(suff[i]) → all right elements
```

So multiplication gives:

```
ALL ELEMENTS EXCEPT nums[i]
```

---

# 🔥 WHY THIS WORKS (CORE INTUITION)

Instead of removing an element,

we build multiplication **around it**.

Think like:

```
Skip middle automatically
```

```
LEFT × RIGHT
```

Middle element never included.

---

# 🧩 Visualization

For index `i`:

```
[ L L L | X | R R R ]

pre[i]  → LLL
suff[i] → RRR

answer = LLL × RRR
```

Element `X` disappears naturally ✅

---

# 🚫 Why Division Not Needed?

Normally:

```
totalProduct / nums[i]
```

But division fails when:

```
nums contains 0
```

Prefix + Suffix works even with zeros.

---

# ⚡ Time Complexity

```
O(n)
```

Three linear passes.

---

# 💾 Space Complexity

```
O(n)
```

(for prefix + suffix arrays)

---

# 🚀 Interview Optimization (Next Level)

We can reduce space to:

```
O(1) extra space
```

by reusing output array.

(This is FAANG expected follow-up.)

---

# 🏆 Final Mental Model

You are NOT calculating product again.

You are pre-storing:

```
Left influence
Right influence
```

Then merging them.

---

🔥 Golden Line:

```
Product Except Self =
Left Product × Right Product
```

---

