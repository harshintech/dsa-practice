# 📚 Course Schedule III (Greedy + Max Heap)

---

🔗 **Repository Link:**  
## [Interview-Preparation GitHub Repo Contribute Now 🕊️.](https://github.com/harshintech/Interview-Preparation)


## 📌 Problem

You are given an array `courses` where:

```
courses[i] = [duration, lastDay]
```

- `duration` → days required to complete the course  
- `lastDay` → deadline by which course must be finished  

Return the **maximum number of courses** you can take.

---

## 🧩 Example

Input:
```
courses = [[100,200],[200,1300],[1000,1250],[2000,3200]]
```

Output:
```
3
```

---

# 🚀 Approach (Greedy + Max Heap)

---

## 🔑 Step 1: Sort by Deadline

```java
Arrays.sort(courses,(a,b)-> a[1] - b[1]);
```

Why?

Because earlier deadlines should be handled first.

If we miss early deadline, future courses don’t matter.

---

## 🔑 Step 2: Use Max Heap

We store:

```
durations of selected courses
```

Why max heap?

If total time exceeds deadline,
we remove the **longest duration course**.

Removing the longest frees maximum time.

---

# 💻 Java Code

```java
class Solution {
    public int scheduleCourse(int[][] courses) {

        Arrays.sort(courses,(a,b)-> a[1] - b[1]);

        PriorityQueue<Integer> pq =
            new PriorityQueue<>((a,b) -> b - a);

        int time = 0;

        for(int[] course : courses){

            time += course[0];
            pq.add(course[0]);

            if(time > course[1])
                time -= pq.poll();
        }

        return pq.size();
    }
}
```

---

# 🎯 Why This Greedy Works

At each course:

1. Take it (add duration)
2. If deadline exceeded:
   - Remove the longest course taken so far

This ensures:

```
We keep maximum number of short-duration courses.
```

---

# 🧠 Dry Run

Input:
```
[[100,200],
 [200,1300],
 [1000,1250],
 [2000,3200]]
```

Sorted by deadline:

```
[100,200]
[1000,1250]
[200,1300]
[2000,3200]
```

Process:

1️⃣ Take 100 → time = 100  
2️⃣ Take 1000 → time = 1100  
3️⃣ Take 200 → time = 1300  
4️⃣ Take 2000 → time = 3300 ❌ exceeds 3200  

Remove longest (2000)

Final courses taken:
```
3
```

---

# ⏱ Time Complexity

Sorting:
```
O(n log n)
```

Heap operations:
```
O(n log n)
```

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

# 🔥 Pattern Used

Greedy  
Sort by Deadline  
Max Heap Removal Strategy  

---

# 🧠 Core Insight

If schedule exceeds limit:

```
Remove the most expensive decision
```

Very powerful greedy pattern.

---

# 🏆 Similar Problems

- IPO (Maximized Capital)
- Minimum Refueling Stops
- Task Scheduler
- Reorganize String

All use:

```
Greedy + Heap
```

---

# ✅ Final Output

Input:
```
[[100,200],[200,1300],[1000,1250],[2000,3200]]
```

Output:
```
3
```

