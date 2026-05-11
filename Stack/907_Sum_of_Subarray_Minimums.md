# 📉 Sum of Subarray Minimums

---

## 📌 Problem

For every possible subarray:

1. Find its minimum element.
2. Add all those minimums together.

Return the total modulo:

```text
1,000,000,007
```

---

## ✅ Example

Input:

```text
arr = [3, 1, 2, 4]
```

Subarrays and minimums:

```text
[3]       → 3
[3,1]     → 1
[3,1,2]   → 1
[3,1,2,4] → 1
[1]       → 1
[1,2]     → 1
[1,2,4]   → 1
[2]       → 2
[2,4]     → 2
[4]       → 4
```

Total:

```text
17
```

---

## ✅ Code (UNCHANGED)

```java
class Solution {

    public int[] getNSL(int[] arr, int n) {

        int[] result = new int[n];
        Stack<Integer> st = new Stack<>();

        for (int i = 0; i < n; i++) {

            while (!st.isEmpty() && arr[st.peek()] >= arr[i]) {
                st.pop();
            }

            result[i] = st.isEmpty() ? -1 : st.peek();

            st.push(i);
        }

        return result;
    }

    public int[] getNSR(int[] arr, int n) {

        int[] result = new int[n];
        Stack<Integer> st = new Stack<>();

        for (int i = n - 1; i >= 0; i--) {

            while (!st.isEmpty() && arr[st.peek()] > arr[i]) {
                st.pop();
            }

             result[i] = st.isEmpty() ? n : st.peek();

            st.push(i);
        }

        return result;
    }

    public int sumSubarrayMins(int[] arr) {
        int n = arr.length;

        int[] NSL = getNSL(arr, n);
        int[] NSR = getNSR(arr, n);

        long sum = 0;
        long M = 1000000007;

        for (int i = 0; i < n; i++) {
            long ls = i - NSL[i];
            long rs = NSR[i] - i;

            long totalWays = ls * rs;
            long totalSum = (long) arr[i] * totalWays;
            sum = (sum + totalSum) % M;

        }

        return (int) sum;
    }
}
```

---

# 🧠 Core Idea

Instead of generating all subarrays, we ask:

```text
For each element arr[i],
in how many subarrays is it the minimum?
```

Then contribution of `arr[i]` is:

```text
arr[i] × number of such subarrays
```

---

# 🎯 Main Formula

```text
Contribution = arr[i] × ls × rs
```

Where:

- `ls` = choices on the left
- `rs` = choices on the right

---

# 🔍 NSL (Nearest Smaller to Left)

For each index `i`, find the nearest index on the left with a strictly smaller value.

If none exists:

```text
-1
```

---

# 🔍 NSR (Nearest Smaller to Right)

For each index `i`, find the nearest index on the right with a smaller-or-equal boundary handling.

If none exists:

```text
n
```

---

# ⚠️ Why Different Comparisons?

## NSL

```java
arr[st.peek()] >= arr[i]
```

## NSR

```java
arr[st.peek()] > arr[i]
```

This asymmetry avoids double counting when duplicates exist.

---

# 📊 Example

```text
arr = [3,1,2,4]
```

---

## NSL

```text
[-1, -1, 1, 2]
```

---

## NSR

```text
[1, 4, 4, 4]
```

---

# 🧮 Contribution Calculation

---

## i = 0, arr[i] = 3

```text
ls = 0 - (-1) = 1
rs = 1 - 0 = 1
ways = 1 × 1 = 1
contribution = 3
```

---

## i = 1, arr[i] = 1

```text
ls = 1 - (-1) = 2
rs = 4 - 1 = 3
ways = 2 × 3 = 6
contribution = 6
```

---

## i = 2, arr[i] = 2

```text
ls = 2 - 1 = 1
rs = 4 - 2 = 2
ways = 2
contribution = 4
```

---

## i = 3, arr[i] = 4

```text
ls = 3 - 2 = 1
rs = 4 - 3 = 1
ways = 1
contribution = 4
```

---

## Final Answer

```text
3 + 6 + 4 + 4 = 17
```

---

# 🧠 Why `ls × rs` Works

Suppose:

```text
ls = 2
rs = 3
```

You can choose:

- 2 possible starting points
- 3 possible ending points

Total combinations:

```text
2 × 3 = 6 subarrays
```

---

# ⏱ Complexity

### Time

```text
O(n)
```

Each element is pushed and popped at most once.

### Space

```text
O(n)
```

For stacks and arrays.

---

# 🏆 Pattern Recognition

If problem asks:

- Sum of minimums / maximums
- Contribution of each element
- Nearest smaller/greater

Think:

```text
Monotonic Stack + Contribution Technique
```

---
