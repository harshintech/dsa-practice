# 🖼 Flip and Invert Image

---

## 📌 Problem

You are given a binary matrix `image`.

You must:

1️⃣ Flip the image horizontally  
2️⃣ Invert the image  

---

## 🔄 What Does That Mean?

### Step 1: Flip Horizontally  
Reverse each row.

Example:
```
[1,0,0]  →  [0,0,1]
```

---

### Step 2: Invert  
Replace:

```
0 → 1
1 → 0
```

Example:
```
[0,0,1]  →  [1,1,0]
```

---

## 🧩 Example

Input:
```
image = [
 [1,1,0],
 [1,0,1],
 [0,0,0]
]
```

After Flip:
```
[
 [0,1,1],
 [1,0,1],
 [0,0,0]
]
```

After Invert:
```
[
 [1,0,0],
 [0,1,0],
 [1,1,1]
]
```

---

# 🚀 Optimized Approach (Flip + Invert Together)

Instead of doing:

- Flip first
- Then invert

We do both **in one pass**.

---

# 💻 Java Code

```java
class Solution {
    public int[][] flipAndInvertImage(int[][] image) {

        int n = image.length;

        for(int i = 0; i < n; i++){

            int left = 0;
            int right = n - 1;

            while(left <= right){

                int temp = image[i][left];

                image[i][left] = image[i][right] ^ 1;
                image[i][right] = temp ^ 1;

                left++;
                right--;
            }
        }

        return image;
    }
}
```

---

# 🧠 Why `^ 1` Works?

XOR with 1 flips bit:

| Value | XOR 1 | Result |
|--------|--------|--------|
| 0 | 0 ^ 1 | 1 |
| 1 | 1 ^ 1 | 0 |

So:

```
value ^ 1 = inverted value
```

Very efficient.

---

# 🎯 Why `left <= right`?

Because:

If row length is odd,  
middle element must also be inverted.

Example:
```
[1,0,1]
```

Middle index needs inversion too.

---

# 🔥 What Is Happening Inside Loop?

For each row:

```
Swap left & right
AND invert both
```

Example:

```
1 0 0
```

Step:

```
Swap 1 and 0 → 0 0 1
Invert → 1 1 0
```

---

# ⏱ Time Complexity

Matrix size:

```
n × n
```

Each element processed once:

```
O(n²)
```

---

# 📦 Space Complexity

```
O(1)
```

In-place modification.

---

# 🏆 Pattern Used

Two Pointers  
Bit Manipulation (XOR)  
In-place Matrix Modification  

---

# ⚡ Interview Insight

This is testing:

- Matrix traversal
- Two pointer logic
- XOR trick knowledge
- In-place optimization

---

# ✅ Final Output

Input:
```
[[1,1,0],[1,0,1],[0,0,0]]
```

Output:
```
[[1,0,0],[0,1,0],[1,1,1]]
```

---


