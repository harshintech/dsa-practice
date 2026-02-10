# 🧠 Search in 2D Matrix II (Row & Column Sorted)

---

## 📌 Problem

You are given a matrix where:

1. Each row is sorted in ascending order.
2. Each column is sorted in ascending order.

Return `true` if `target` exists, otherwise `false`.

---

## 🧩 Example

Input:

```
matrix = [
  [1,  4,  7, 11, 15],
  [2,  5,  8, 12, 19],
  [3,  6,  9, 16, 22],
  [10,13, 14,17, 24],
  [18,21, 23,26, 30]
]

target = 5
```

Output:
```
true
```

---

# 🚀 Approach (Top-Right Corner Trick)

## 🔑 Key Idea

Start from **top-right corner**.

Why?

Because at position `(row, col)`:

- Left side → smaller values
- Down side → larger values

So we can eliminate:

- One row
OR
- One column

in every step.

---

# 💻 Java Code

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {

        int n = matrix.length;
        int m = matrix[0].length;

        int row = 0;
        int col = m - 1;

        while (row < n && col >= 0) {

            if (matrix[row][col] == target) {
                return true;

            } else if (matrix[row][col] < target) {
                row++;      // move down
            } else {
                col--;      // move left
            }
        }

        return false;
    }
}
```

---

# 🎨 Why Start From Top-Right?

Example:

```
1   4   7  11
2   5   8  12
3   6   9  16
```

Start at:

```
11  (row=0, col=3)
```

If:

- 11 < target → move down
- 11 > target → move left

You eliminate either:

- Entire row
OR
- Entire column

Each move reduces search space.

---

# 🎯 Dry Run

Target = 5

Start at 15

15 > 5 → move left  
11 > 5 → move left  
7  > 5 → move left  
4  < 5 → move down  
5  == 5 → found ✅

---

# ⏱ Time Complexity

```
O(n + m)
```

Worst case:

- Move at most `n` times down
- Move at most `m` times left

---

# 📦 Space Complexity

```
O(1)
```

No extra space used.

---

# 🔥 Pattern Used

Matrix Search  
Two Pointer (Row + Column)  
Greedy Elimination  

---

# ⚠ Important Difference

This approach works when:

- Rows sorted
- Columns sorted

But NOT necessarily globally sorted.

If matrix is fully sorted like 1D array,
use Binary Search method (log(n×m)).

---

# 🧠 When To Use Which?

| Matrix Type | Best Approach |
|-------------|--------------|
| Fully sorted like 1D | Binary Search |
| Row & Column sorted | Top-Right Trick |

---

# ✅ Final Output

Input:
```
matrix as above
target = 20
```

Output:
```
false
```

