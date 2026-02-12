# LeetCode 347 - Top K Frequent Elements (Min Heap Approach)

---

## 📌 Problem

Given an integer array `nums` and an integer `k`,  
return the `k` most frequent elements.

You may return the answer in any order.

---

## 🧩 Example

Input:
```
nums = [1,1,1,2,2,3]
k = 2
```

Output:
```
[1,2]
```

Because:

```
1 → 3 times
2 → 2 times
3 → 1 time
```

Top 2 frequent → 1 and 2.

---

# 🚀 Approach (HashMap + Min Heap)

## 🔑 Key Idea

1. Count frequency using HashMap.
2. Maintain a **Min Heap of size k**.
3. If heap size exceeds k → remove smallest frequency.
4. In the end → heap contains top k frequent elements.

---

# 💻 Java Code

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {

        Map<Integer,Integer> map = new HashMap<>();

        // Step 1: Count frequency
        for(int num: nums){
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        // Step 2: Min Heap (based on frequency)
        PriorityQueue<Integer> minHeap =
                new PriorityQueue<>((a, b) -> map.get(a) - map.get(b));

        for(int num : map.keySet()){
            minHeap.add(num);

            if(minHeap.size() > k){
                minHeap.poll();
            }
        }

        // Step 3: Build result
        int[] res = new int[k];
        int i = 0;

        while(!minHeap.isEmpty()){
            res[i++] = minHeap.poll();
        }

        return res;
    }
}
```

---

# 🎯 Why Min Heap?

We keep only `k` elements.

Heap stores smallest frequency at top.

If size > k:
```
Remove smallest frequency
```

So only top k frequent remain.

---

# 🧠 Dry Run

Input:
```
nums = [1,1,1,2,2,3]
k = 2
```

Frequency Map:
```
1 → 3
2 → 2
3 → 1
```

Heap process:

Add 1  
Add 2  
Add 3 → size becomes 3 → remove smallest (3)

Final heap:
```
[1,2]
```

---

# ⏱ Time Complexity

```
O(n log k)
```

Where:
- n = number of elements
- Heap size is k

---

# 📦 Space Complexity

```
O(n)
```

For frequency map.

---

# 🔥 Pattern Used

HashMap for Frequency  
Min Heap for Top K  
Heap Size Control  

---

# ⚠ Why Not Max Heap?

Max heap would require:

```
O(n log n)
```

But min heap of size k:

```
O(n log k)
```

More efficient when k << n.

---

# 🏆 Interview Insight

Whenever problem says:

> Top K something

Think:

- Min Heap of size K  
OR  
- Bucket Sort  
OR  
- Quick Select  

---

# 🚀 Optimal Alternative (O(n))

Bucket Sort approach:

- Create array of lists (size n+1)
- Index = frequency
- Traverse from high frequency to low

Time Complexity:
```
O(n)
```

---

# ✅ Final Output

Input:
```
[1,1,1,2,2,3], k=2
```

Output:
```
[1,2]
```

