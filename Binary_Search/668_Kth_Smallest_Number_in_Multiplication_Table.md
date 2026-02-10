# 🧠 Kth Smallest Number in Multiplication Table

---

## 📌 Problem

You are given:

- `m` → number of rows  
- `n` → number of columns  
- A multiplication table of size `m × n`

Return the **kth smallest number** in the multiplication table.

---

## 🧩 Example

Input:
```
m = 3
n = 3
k = 5
```

Multiplication Table:

```
1  2  3
2  4  6
3  6  9
```

Sorted order:
```
1 2 2 3 3 4 6 6 9
```

Output:
```
3
```

---

# 🚀 Approach (Binary Search on Answer)

## 🔑 Key Idea

We DO NOT generate the entire table.

Instead, we binary search on value range:

```
low = 1
high = m * n
```

For every `mid`, count:

```
How many numbers ≤ mid ?
```

If count < k → answer is bigger  
If count ≥ k → answer is smaller or equal  

---

# 💻 Java Code

```java
class Solution {
    public int findKthNumber(int m, int n, int k) {

        int low = 1;
        int high = m * n;

        // TC : O(m * log(m*n))

        while(low < high){

            int mid = low + (high - low) / 2;

            int count = 0;  

            // Count numbers <= mid
            for(int i = 1; i <= m; i++){
                count += Math.min(mid / i, n);
            }

            if(count < k){
                low = mid + 1;
            } else {
                high = mid;
            }
        }

        return low;
    }
}
```

---

# 🎯 Why count += Math.min(mid / i, n) ?

In row `i`, values are:

```
i, 2i, 3i, 4i ... ni
```

If we want numbers ≤ mid:

```
mid / i
```

gives how many multiples fit.

But row only has `n` columns.

So we take:

```
Math.min(mid / i, n)
```

---

# 🧠 Dry Run

Example:

```
m = 3
n = 3
k = 5
```

Range:
```
1 → 9
```

Try mid = 5

Count numbers ≤ 5:

Row 1:
```
5 / 1 = 5 → min(5,3) = 3
```

Row 2:
```
5 / 2 = 2 → min(2,3) = 2
```

Row 3:
```
5 / 3 = 1 → min(1,3) = 1
```

Total count = 3 + 2 + 1 = 6

6 ≥ 5 → try smaller

Eventually answer becomes:
```
3
```

---

# ⏱ Time Complexity

```
O(m * log(m*n))
```

- Binary search runs log(m*n) times
- Counting takes O(m)

---

# 📦 Space Complexity

```
O(1)
```

---

# 🔥 Pattern Used

Binary Search on Answer  
Counting in Multiplication Table  
Monotonic Condition  

---

# ⚠ Important Notes

- We are searching value space, not index.
- Duplicates exist (like 6 appears twice).
- We use lower bound logic.

---

# 🏆 Interview Insight

This is classic example of:

```
Binary Search on Answer + Mathematical Counting
```

Similar to:

- Kth smallest in sorted matrix
- Koko eating bananas
- Ship capacity problem

---

# ✅ Final Output

Input:
```
m = 3, n = 3, k = 5
```

Output:
```
3
```
![itachiuchiha.png](https://assets.leetcode.com/users/images/99ea11f3-858f-4804-b622-da2f1722941a_1770748431.1022782.png)

