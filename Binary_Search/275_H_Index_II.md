# 🧠 H-Index II (Sorted Array – Binary Search)

---

## 📌 Problem

You are given an array `citations[]` sorted in **ascending order**.

Return the researcher's **h-index**.

### 📖 Definition of H-Index

A researcher has index `h` if:

- `h` papers have **at least h citations each**.

---

## 🧩 Example

Input:
```
citations = [0,1,3,5,6]
```

Output:
```
3
```

Explanation:

There are 3 papers with at least 3 citations.

---

# 🚀 Approach (Binary Search on Index)

## 🔑 Key Idea

Since array is sorted:

If we pick index `mid`, then:

```
Number of papers to the right = n - mid
```

So we check:

```
citations[mid] >= n - mid
```

If true:

- This index might give valid h-index.
- Try to find smaller index for possibly larger answer.

If false:

- Move right.

---

# 💻 Java Code

```java
class Solution {
    public int hIndex(int[] citations) {

        int n = citations.length;
        int low = 0;
        int high = n - 1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (citations[mid] >= n - mid) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }

        return n - low;
    }
}
```

---

# 🎨 Step-by-Step Dry Run

Input:
```
[0,1,3,5,6]
```

n = 5

---

### Step 1

low = 0  
high = 4  

mid = 2  

```
citations[2] = 3
n - mid = 5 - 2 = 3
```

3 ≥ 3 ✅

Move left:
```
high = 1
```

---

### Step 2

low = 0  
high = 1  

mid = 0  

```
citations[0] = 0
n - mid = 5
```

0 ≥ 5 ❌

Move right:
```
low = 1
```

---

### Step 3

low = 1  
high = 1  

mid = 1  

```
citations[1] = 1
n - mid = 4
```

1 ≥ 4 ❌

Move right:
```
low = 2
```

Loop ends.

Return:
```
n - low = 5 - 2 = 3
```

---

# 🧠 Why Return `n - low`?

At the end:

- `low` points to first valid position
- Papers from `low → end` satisfy condition

Count of such papers:

```
n - low
```

That is the maximum h-index.

---

# ⏱ Time Complexity

O(log n)

Binary search.

---

# 📦 Space Complexity

O(1)

Only variables used.

---

# 🔥 Pattern Used

Binary Search on Index  
Monotonic Condition  
Sorted Array Optimization  

---

# ⚠ Important

This solution works only when:

```
citations array is sorted
```

If unsorted → need different approach (counting or sorting first).

---

# 🏆 Interview Insight

We are binary searching for the **first index** where:

```
citations[mid] >= n - mid
```

This is similar to:

- Lower bound problems
- First true in monotonic condition

---

# ✅ Final Output

Input:
```
[0,1,3,5,6]
```

Output:
```
3
```

