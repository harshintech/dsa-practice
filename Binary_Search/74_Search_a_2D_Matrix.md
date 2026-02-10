# 🧠 Search a 2D Matrix (Binary Search)

---

## 📌 Problem

You are given a 2D matrix where:

1. Each row is sorted in ascending order.
2. The first element of each row is greater than the last element of previous row.

Return `true` if `target` exists in the matrix, otherwise `false`.

---

## 🧩 Example

Input:

```
matrix = [
  [1, 3, 5, 7],
  [10,11,16,20],
  [23,30,34,60]
]

target = 3
```

Output:

```
true
```

---

# 🚀 Key Idea

Since:

- Rows are sorted
- Entire matrix behaves like a sorted array

We can treat the matrix as a **1D sorted array** of size:

```
n × m
```

Then apply **Binary Search**.

---

# 🧠 How We Convert 1D Index → 2D Index

If:

```
mid = some index in imaginary 1D array
```

Then:

```
row = mid / m
col = mid % m
```

Where:

- `m` = number of columns

---

# 💻 Java Code

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {

        int n = matrix.length;
        int m = matrix[0].length;

        int low = 0;
        int high = (n * m) - 1;

        // TC : O(log(n × m))
        // SC : O(1)

        while(low <= high){

            int mid = low + (high - low) / 2;

            int row = mid / m;
            int col = mid % m;

            if(matrix[row][col] == target)
                return true;

            if(matrix[row][col] < target){
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return false;
    }
}
```

---

# 🎨 Dry Run

Matrix:

```
1   3   5   7
10  11  16  20
23  30  34  60
```

Target = 16

Total elements:

```
3 × 4 = 12
```

Range:

```
0 → 11
```

---

### Step 1

mid = 5  

```
row = 5 / 4 = 1
col = 5 % 4 = 1
```

matrix[1][1] = 11  

11 < 16 → move right

---

### Step 2

mid = 8  

```
row = 8 / 4 = 2
col = 8 % 4 = 0
```

matrix[2][0] = 23  

23 > 16 → move left

---

### Step 3

mid = 6  

```
row = 6 / 4 = 1
col = 6 % 4 = 2
```

matrix[1][2] = 16  

Found ✅

---

# ⏱ Time Complexity

```
O(log(n × m))
```

Binary search on total elements.

---

# 📦 Space Complexity

```
O(1)
```

No extra space used.

---

# 🔥 Pattern Used

Binary Search on Virtual 1D Array  
Index Mapping Trick  

---

# 🧠 Why This Is Powerful

Instead of:

- First finding row
- Then searching column

We directly treat matrix as sorted array.

Clean and optimal.

---

# ⚠ Important Condition

This works ONLY when:

```
matrix[i][0] > matrix[i-1][last]
```

If rows are sorted but not globally sorted,
you need different approach.

---

# ✅ Final Output

Input:
```
matrix = [[1,3,5],[7,9,11]]
target = 9
```

Output:
```
true
```

