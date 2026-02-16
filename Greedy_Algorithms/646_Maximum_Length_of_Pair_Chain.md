# 🔗 Maximum Length of Pair Chain (Greedy)

---

## 📌 Problem

You are given an array of pairs:

```
pairs[i] = [a, b]
```

A pair `[c, d]` can follow `[a, b]` if:

```
b < c
```

Return the **length of the longest chain** you can form.

---

## 🧩 Example

Input:
```
pairs = [[1,2],[2,3],[3,4]]
```

Output:
```
2
```

Valid chain:
```
[1,2] → [3,4]
```

We cannot use `[2,3]` after `[1,2]`
because:

```
2 is NOT < 2
```

---

# 🚀 Approach (Greedy – Sort by Ending Time)

---

## 🔑 Core Idea

This is exactly like:

```
Activity Selection Problem
```

Strategy:

1️⃣ Sort pairs by second element (ending time)  
2️⃣ Always pick the pair that ends earliest  
3️⃣ Then pick the next valid pair  

This ensures maximum chain length.

---

# 💻 Java Code

```java
class Solution {
    public int findLongestChain(int[][] pairs) {

        Arrays.sort(pairs,
            Comparator.comparingInt(a -> a[1]));

        int[] prev = pairs[0];
        int res = 1;

        for (int i = 1; i < pairs.length; i++) {

            int[] cur = pairs[i];

            if (prev[1] < cur[0]) {
                res++;
                prev = cur;
            }
        }

        return res;
    }
}
```

---

# 🎯 Why Sort by Second Element?

If we sort by starting time, greedy may fail.

Sorting by ending time ensures:

```
We leave maximum space for future pairs.
```

Same logic as:

- Meeting Rooms
- Activity Selection
- Non-overlapping intervals

---

# 🧠 Dry Run

Input:
```
[[1,2],[2,3],[3,4]]
```

After sorting by end:

```
[1,2]
[2,3]
[3,4]
```

Start:

```
prev = [1,2]
res = 1
```

Check [2,3]:
```
2 < 2 ❌
```

Check [3,4]:
```
2 < 3 ✔
res = 2
```

Final answer:
```
2
```

---

# ⏱ Time Complexity

Sorting:
```
O(n log n)
```

Traversal:
```
O(n)
```

Total:
```
O(n log n)
```

---

# 📦 Space Complexity

```
O(1)
```

(ignoring sorting internal space)

---

# 🔥 Pattern Used

Greedy  
Sort by End Time  
Interval Scheduling  

---

# 🏆 Why Greedy Works?

By choosing the pair that finishes earliest:

We maximize remaining available range.

Classic greedy proof from activity selection.

---

# 🧠 Interview Insight

This is strongly related to:

- Non-overlapping Intervals
- Minimum Arrows to Burst Balloons
- Meeting Rooms II
- Course Schedule III

All use:

```
Sort + Greedy
```

---

# ✅ Final Output

Input:
```
[[1,2],[2,3],[3,4]]
```

Output:
```
2
```

---


