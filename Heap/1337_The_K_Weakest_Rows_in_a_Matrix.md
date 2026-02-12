# 🧠 The K Weakest Rows in a Matrix

---

## 📌 Problem

You are given a matrix `mat` where:

- 1 → soldier  
- 0 → civilian  
- Soldiers always appear before civilians in each row  

Return the indices of the `k` weakest rows in the matrix.

### Weakness Rule:

1. Row with fewer soldiers is weaker.
2. If equal soldiers → smaller index is weaker.

---

## 🧩 Example

Input:
```
mat = [
 [1,1,0,0,0],
 [1,1,1,1,0],
 [1,0,0,0,0],
 [1,1,0,0,0],
 [1,1,1,1,1]
]
k = 3
```

Output:
```
[2,0,3]
```

Because:

```
Row 2 → 1 soldier
Row 0 → 2 soldiers
Row 3 → 2 soldiers
Row 1 → 4 soldiers
Row 4 → 5 soldiers
```

---

# 🚀 Approach (Binary Search + Max Heap of Size K)

## 🔑 Key Idea

Step 1 → Count soldiers in each row using **Binary Search**  
Step 2 → Maintain a **Max Heap of size k**  

Why max heap?

Because we want to remove strongest row when heap size > k.

---

# 💻 Java Code

```java
class Solution {
    public int[] kWeakestRows(int[][] mat, int k) {

        PriorityQueue<int[]> maxHeap = new PriorityQueue<>((a, b) -> {
            if (a[0] != b[0]) {
                return b[0] - a[0]; // Compare soldier count
            } else {
                return b[1] - a[1]; // Compare index
            }
        });

        for(int i = 0; i < mat.length; i++){

            int soldiers = countSoldiers(mat[i]);

            maxHeap.offer(new int[]{soldiers, i});

            if (maxHeap.size() > k) {
                maxHeap.poll();
            }
        }

        int[] result = new int[k];

        for (int i = k - 1; i >= 0; i--) {
            result[i] = maxHeap.poll()[1];
        }

        return result;
    }

    private int countSoldiers(int[] arr){

        int low = 0;
        int high = arr.length;

        while(low < high){

            int mid = low + (high - low) / 2;

            if(arr[mid] == 1)
                low = mid + 1;
            else
                high = mid;
        }

        return low;
    }
}
```

---

# 🎯 Why Binary Search Works?

Each row looks like:

```
1 1 1 1 0 0 0
```

We find first 0.

Index of first 0 = number of soldiers.

Binary search time:
```
O(log m)
```

---

# 🧠 Why Max Heap?

Heap stores:

```
[soldierCount, rowIndex]
```

Comparator:

- Higher soldier count → stronger
- If tie → higher index → stronger

So strongest row stays at top.

When size > k → remove strongest.

At end → heap contains k weakest rows.

---

# ⏱ Time Complexity

Counting soldiers:
```
O(n log m)
```

Heap operations:
```
O(n log k)
```

Total:
```
O(n log m + n log k)
```

---

# 📦 Space Complexity

```
O(k)
```

---

# 🔥 Pattern Used

Binary Search inside Row  
Top K Pattern  
Max Heap of Size K  
Custom Comparator  

---

# ⚠ Why Fill Result from Back?

Because max heap gives strongest first.

We want weakest first.

So:

```
result[i] = maxHeap.poll()[1]
```

starting from end.

---

# 🏆 Interview Insight

This problem combines:

- Binary Search
- Heap
- Comparator logic
- Top K Pattern

Very strong interview combination.

---

# ✅ Final Output

Input:
```
k = 3
```

Output:
```
[2,0,3]
```

