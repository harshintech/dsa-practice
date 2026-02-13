# LeetCode 1046 - Last Stone Weight (Max Heap Approach)

---

## 📌 Problem

You are given an array `stones[]`.

Each turn:

1. Pick the two heaviest stones.
2. Smash them.
3. If equal → both destroyed.
4. If not equal → push back the difference.

Return the weight of the last remaining stone.  
If none left → return `0`.

---

## 🧩 Example

Input:
```
stones = [2,7,4,1,8,1]
```

Process:

```
8 - 7 = 1  → [2,4,1,1,1]
4 - 2 = 2  → [2,1,1,1]
2 - 1 = 1  → [1,1,1]
1 - 1 = 0  → [1]
```

Output:
```
1
```

---

# 🚀 Approach (Max Heap)

## 🔑 Key Idea

We always need the **two largest stones**.

So we use:

```
Max Heap (PriorityQueue with reverse order)
```

Each iteration:

- Extract two largest
- If different → push difference

---

# 💻 Java Code

```java
class Solution {
    public int lastStoneWeight(int[] stones) {

        PriorityQueue<Integer> pq =
            new PriorityQueue<>(Collections.reverseOrder());

        for (int stone : stones) {
            pq.add(stone);
        }

        // TC = O(n log n)
        // SC = O(n)

        while (pq.size() > 1) {

            int stone1 = pq.poll();
            int stone2 = pq.poll();

            if (stone1 != stone2) {
                pq.add(stone1 - stone2);
            }
        }

        return pq.size() == 0 ? 0 : pq.peek();
    }
}
```

---

# 🎯 Why Max Heap?

Because:

We must always get:

```
Largest stone
Second largest stone
```

Max heap gives that in:

```
O(log n)
```

---

# ⏱ Time Complexity

### Building heap:
```
O(n)
```

### Each poll/add:
```
O(log n)
```

In worst case, we do this n times.

Total:
```
O(n log n)
```

---

# 📦 Space Complexity

```
O(n)
```

For heap.

---

# 🔥 Why Brute Force is Bad?

Brute force approach:

1. Sort every time
2. Remove two largest
3. Insert difference
4. Repeat

Time:

```
n log n + (n-1) log(n-1) + ...
≈ O(n² log n)
```

Much slower.

---

# 🧠 Pattern Used

Heap  
Repeated Maximum Extraction  
Simulation  

---

# ⚠ Alternative Comparator

Instead of:

```java
Collections.reverseOrder()
```

You can use:

```java
(a, b) -> b - a
```

Both create max heap.

---

# 🏆 Interview Insight

Whenever problem says:

> Repeatedly take largest elements

Think:

```
Max Heap
```

Whenever problem says:

> Repeatedly take smallest elements

Think:

```
Min Heap
```

---

# ✅ Final Output

Input:
```
[2,7,4,1,8,1]
```

Output:
```
1
```


