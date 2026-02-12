# 🧠 K Closest Points to Origin (Max Heap Approach)

---

## 📌 Problem

Given an array of points on a 2D plane:

```
points[i] = [xi, yi]
```

Return the `k` closest points to the origin `(0,0)`.

Distance formula:

```
√(x² + y²)
```

⚠ We can ignore square root because comparison works on squared distance.

---

## 🧩 Example

Input:
```
points = [[1,3],[-2,2]]
k = 1
```

Output:
```
[[-2,2]]
```

Because:

```
Distance(1,3)  = 1² + 3² = 10
Distance(-2,2) = 4 + 4 = 8
```

8 < 10 → closer.

---

# 🚀 Approach (Max Heap of Size K)

## 🔑 Key Idea

We want the **k smallest distances**.

So we use:

```
Max Heap of size k
```

Why max heap?

Because:

- If heap size exceeds k,
- Remove the farthest point.

So only k closest remain.

---

# 💻 Java Code

```java
class Solution {
    public int[][] kClosest(int[][] points, int k) {

        PriorityQueue<int[]> maxHeap =
            new PriorityQueue<>((a, b) -> getDistance(b) - getDistance(a));

        for(int[] point : points){

            maxHeap.add(point);

            if(maxHeap.size() > k){
                maxHeap.poll();
            }
        }

        int[][] res = new int[k][2];

        while(k > 0){
            res[--k] = maxHeap.poll();
        }

        return res;
    }

    private int getDistance(int[] point) {
        return point[0] * point[0] + point[1] * point[1];
    }
}
```

---

# 🎯 Why Max Heap?

We maintain heap size = k.

If a new point comes:

- If closer → it stays
- If farther → it gets removed

So heap always stores k closest.

---

# 🧠 Dry Run

Input:
```
points = [[3,3],[5,-1],[-2,4]]
k = 2
```

Distances:
```
(3,3) → 18
(5,-1) → 26
(-2,4) → 20
```

Process:

Add (3,3)  
Add (5,-1)  
Add (-2,4) → size > 2 → remove farthest (5,-1)

Final heap:
```
(3,3), (-2,4)
```

---

# ⏱ Time Complexity

```
O(n log k)
```

Where:
- n = number of points

---

# 📦 Space Complexity

```
O(k)
```

Heap stores only k elements.

---

# 🔥 Pattern Used

Top K Pattern  
Max Heap of Size K  
Distance Calculation Optimization  

---

# ⚠ Important Optimization

We use:

```
x² + y²
```

Instead of:

```
√(x² + y²)
```

Because square root is unnecessary for comparison.

---

# 🏆 Alternative Approach

You can also use:

- QuickSelect (Average O(n))
- Sorting (O(n log n))

But heap is clean and safe.

---

# ✅ Final Output

Input:
```
[[1,3],[-2,2]], k=1
```

Output:
```
[[-2,2]]
```

