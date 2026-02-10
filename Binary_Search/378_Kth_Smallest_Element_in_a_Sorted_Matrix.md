# LeetCode 378 - Kth Smallest Element in a Sorted Matrix

---

## 📌 Problem

You are given an `n x n` matrix where:

- Each row is sorted in ascending order.
- Each column is sorted in ascending order.

Return the **kth smallest element** in the matrix.

---

## 🧩 Example

Input:
```
matrix = [
 [1, 5, 9],
 [10,11,13],
 [12,13,15]
]

k = 8
```

Output:
```
13
```

---

# 🚀 Approach (Binary Search on Answer)

## 🔑 Key Idea

We do NOT binary search on index.

We binary search on **value range**.

Range:

```
low  = matrix[0][0]
high = matrix[n-1][n-1]
```

For each `mid`, we count:

```
How many elements ≤ mid ?
```

If count < k → answer is bigger  
If count ≥ k → answer is smaller or equal  

---

# 💻 Java Code

```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {

        int n = matrix.length;

        int low = matrix[0][0];
        int high = matrix[n-1][n-1];

        while(low <= high){

            int mid = low + (high - low) / 2;
            int count = countLessorEqual(matrix, mid);

            if(count < k){
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return low;   
    }

    public int countLessorEqual(int[][] matrix, int mid){

        int n = matrix.length;
        int row = n - 1;
        int col = 0;    
        int count = 0;

        while(row >= 0 && col < n){

            if(matrix[row][col] <= mid){

                // Add all elements above this in same column
                count += row + 1;
                col++;

            } else {
                row--; 
            }
        }

        return count;
    }
}
```

---

# 🎨 Why count += row + 1 ?

Imagine:

```
1   5   9
10 11  13
12 13  15
```

Start from bottom-left:

If:

```
matrix[row][col] <= mid
```

Since column is sorted:

All elements above it are also ≤ mid.

So instead of counting 1 element:

We add:

```
row + 1
```

Entire column portion.

That makes counting O(n).

---

# 🧠 Dry Run

Example:

```
k = 8
```

Range:
```
1 → 15
```

Try mid = 8

Count elements ≤ 8:
```
1,5
```

Count = 2

Too small → increase low.

Eventually binary search narrows to:

```
13
```

---

# ⏱ Time Complexity

```
O(n log(max-min))
```

- Counting takes O(n)
- Binary search runs log(range) times

---

# 📦 Space Complexity

```
O(1)
```

---

# 🔥 Pattern Used

Binary Search on Answer  
Sorted Matrix Counting  
Monotonic Condition  

---

# ⚠ Important Concept

We are NOT searching index.

We are searching the smallest number such that:

```
count of numbers ≤ x ≥ k
```

This is classic:

```
Lower Bound in Value Space
```

---

# 🏆 When To Use This Pattern?

Whenever:

- Matrix row-wise & column-wise sorted
- Asked for kth smallest / largest
- Value range known

---

# ✅ Final Output

Input:
```
k = 8
```

Output:
```
13
```

---

# 🎯 Interview Insight

This is combination of:

- Matrix trick
- Binary search on answer
- Monotonic counting

High-level question for strong candidates.

