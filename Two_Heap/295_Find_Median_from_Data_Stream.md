# 📊 Find Median from Data Stream

---
🔗 **Repository Link:**  
## [Interview-Preparation GitHub Repo Contribute Now 🕊️.](https://github.com/harshintech/Interview-Preparation)

## 📌 Problem

Design a data structure that supports:

```
addNum(int num)
findMedian()
```

We continuously receive numbers, and at any moment we should be able to return the median.

---

## 🧠 Core Idea

We maintain **two heaps**:

### 🔹 Max Heap (Left Half)
- Stores smaller half of numbers
- Largest of smaller half at top

### 🔹 Min Heap (Right Half)
- Stores larger half of numbers
- Smallest of larger half at top

---

## 🎯 Invariant Rules

1. `maxHeap.size() == minHeap.size()`  
   OR  
   `maxHeap.size() == minHeap.size() + 1`

2. All elements in `maxHeap` ≤ elements in `minHeap`

---

# 💻 Clean & Balanced Implementation (Recommended Version)

```java
class MedianFinder {

    PriorityQueue<Integer> minHeap;
    PriorityQueue<Integer> maxHeap;

    public MedianFinder() {
        minHeap = new PriorityQueue<>();
        maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    }

    public void addNum(int num) {

        // Step 1: Add number to correct heap
        if (maxHeap.isEmpty() || num <= maxHeap.peek()) {
            maxHeap.add(num);
        } else {
            minHeap.add(num);
        }

        // Step 2: Balance the heaps
        if (maxHeap.size() > minHeap.size() + 1) {
            minHeap.add(maxHeap.poll());
        } else if (minHeap.size() > maxHeap.size()) {
            maxHeap.add(minHeap.poll());
        }
    }

    public double findMedian() {

        if (maxHeap.size() == minHeap.size()) {
            return (maxHeap.peek() + minHeap.peek()) / 2.0;
        }

        return maxHeap.peek();
    }
}
```

---

# 🧩 Example

Stream:

```
addNum(1)
addNum(2)
findMedian() → 1.5
addNum(3)
findMedian() → 2
```

---

# 🎨 Visual Representation

After adding 1:
```
MaxHeap: [1]
MinHeap: []
Median = 1
```

After adding 2:
```
MaxHeap: [1]
MinHeap: [2]
Median = (1+2)/2 = 1.5
```

After adding 3:
```
MaxHeap: [2,1]
MinHeap: [3]
Median = 2
```

---

# ⏱ Time Complexity

### addNum:
```
O(log n)
```

### findMedian:
```
O(1)
```

---

# 📦 Space Complexity

```
O(n)
```

---

# 🔥 Why Two Heaps?

Because:

- One heap alone cannot efficiently maintain median.
- Two heaps split data into two balanced halves.

---

# 🏆 Pattern Used

Heap  
Data Stream Processing  
Balancing Strategy  

---

# ⚠ Why This Version Is Cleaner

Your first version manually handled balancing inside conditions.

Second version:

✔ Cleaner  
✔ Easier to reason  
✔ Less bug-prone  
✔ Industry standard  

---

# 🧠 Interview Insight

This is a **very common FAANG question**.

Tests:

- Heap understanding
- Balancing logic
- Data structure design
- Streaming processing

---

# ✅ Final Summary

| Operation | Complexity |
|-----------|------------|
| addNum    | O(log n)   |
| findMedian| O(1)       |

---

