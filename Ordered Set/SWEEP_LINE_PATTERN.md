# 🧹 Sweep Line Algorithm (Complete Guide for Interviews)

## 📌 What is Sweep Line?

Sweep Line is a technique where we:

> Move from left → right over a sorted structure  
> and maintain running information (count, max, sum, etc.)

It is mainly used in **interval / range overlap problems**.

---

# 🧠 Core Idea

Instead of checking all intervals one by one (O(n²)):

We:

1. Mark interval start as `+1`
2. Mark interval end as `-1`
3. Traverse in sorted order
4. Maintain a running prefix sum

This tells us how many intervals are active at any moment.

---

# 🧹 Sweep Line Algorithm – Graphical Explanation

---

## 🟢 Step 1: Draw Timeline

Imagine a number line:

```

0 ---- 5 ---- 10 ---- 15 ---- 20 ---- 25 ---- 30

```

Now consider these intervals:

```

A: 10 -------- 20
B:       15 -------- 25
C: 5 ----- 12

```

### Graphically:

```

Time →

5      10      15      20      25
|------|-------|-------|-------|
C:  =======
A:         ==========
B:               ==========

```

### Question:
👉 At which point maximum overlap hai?

---

## 🟢 Step 2: Convert to Events

Instead of thinking about full ranges,  
we only care about **start and end events**.

- When interval starts → `+1`
- When interval ends → `-1`

So convert intervals into events:

```

5  → +1   (C start)
10 → +1   (A start)
12 → -1   (C end)
15 → +1   (B start)
20 → -1   (A end)
25 → -1   (B end)

```

---

## 🟢 Step 3: Sweep from Left to Right

Now imagine a vertical line moving from left → right.

At each time, maintain a running count:

```

Time 5   → active = 1
Time 10  → active = 2
Time 12  → active = 1
Time 15  → active = 2
Time 20  → active = 1
Time 25  → active = 0

```

### Maximum active = **2**

That’s the answer.

---

# 🔥 Why This Works

Each interval contributes:

- `+1` when it begins
- `-1` when it finishes

So when we keep adding values in sorted order:

We are literally counting:

> "How many intervals are currently alive?"

Prefix sum = number of active intervals.

That is why sweep line works.

---

# 🧠 Deep Understanding

Instead of checking:

```

A overlaps B?
B overlaps C?
A overlaps C?

```

Which takes:

```

O(n²)

```

We transform the problem into:

```

At each point in time,
how many intervals are active?

```

Which becomes:

```

O(n log n)

```

---

# 🎥 Real Life Analogy

Imagine:

- People entering a room → `+1`
- People leaving → `-1`

If we track running count:

We instantly know:

> Maximum number of people inside the room at the same time.

That is sweep line.

---

# 🟡 Why Ordered Map is Needed?

If times are not sorted:

```

15 → +1
5  → +1
10 → +1

````

Prefix sum becomes incorrect.

So in Java we use:

```java
TreeMap<Integer, Integer>
````

Because:

* Keys remain sorted
* Prefix sum works correctly

---

# 🧩 Why It Is Powerful

Sweep line converts:

```
Range Problem
        ↓
Point-based counting problem
        ↓
Prefix sum problem
```

And prefix sum is simple and efficient.

---

# 🟢 One Line Memory Trick

Sweep Line =

> "Main time pe line chala raha hoon aur count kar raha hoon kitne active hain."

---

# 🧩 Generic Java Pattern

```java
TreeMap<Integer, Integer> map = new TreeMap<>();

// Add interval
map.put(start, map.getOrDefault(start, 0) + 1);
map.put(end, map.getOrDefault(end, 0) - 1);

int active = 0;
int maxActive = 0;

for (int value : map.values()) {
    active += value;
    maxActive = Math.max(maxActive, active);
}
```

---

# ⏱ Time Complexity

* Insert → O(log n)
* Sweep → O(n)
* Per operation → O(n)

For small constraints, this is efficient and interview-safe.

---

# 🎯 When Should We Use Sweep Line?

Use this pattern when:
✅ Finding maximum overlapping intervals
✅ Counting active events at any time
✅ Calendar booking problems
✅ Minimum number of meeting rooms
✅ Railway platform problems
✅ Peak resource usage
✅ Detecting triple booking

---

# 🚫 When NOT To Use Sweep Line

❌ When problem is not interval-based
❌ When ordering does not matter
❌ When simple comparison solves it

Sweep Line is specifically useful for:

> Problems involving ranges over time or number line.

---

# 🧠 Key Insight

Instead of comparing intervals pair by pair:

We transform the problem into:

> "How many intervals are active at this point?"

And solve it using prefix sum on ordered data.

---

# 📘 Problems That Use This Pattern

* My Calendar I
* My Calendar II
* My Calendar III
* Meeting Rooms II
* Minimum Platforms

All involve counting overlaps efficiently.

---

# 🟢 Final Summary

Sweep Line Algorithm:

* Convert intervals into start(+1) and end(-1)
* Store in ordered structure
* Traverse in sorted order
* Maintain running count
* Track maximum or validate condition

It is a powerful and clean interview pattern
for solving interval overlap problems.

---


