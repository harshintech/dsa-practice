# LeetCode 871 - 🚗 Minimum Number of Refueling Stops

---

## 📌 Problem

You are driving towards a destination.

Given:

- `target` → total distance to destination  
- `startFuel` → initial fuel  
- `stations[i] = [position, fuel]`  

Each station gives you `fuel` amount.

Return the **minimum number of refueling stops** needed to reach the target.

If impossible → return `-1`.

---

## 🧩 Example

Input:
```
target = 100
startFuel = 10
stations = [[10,60],[20,30],[30,30],[60,40]]
```

Output:
```
2
```

---

# 🚀 Approach (Greedy + Max Heap)

---

## 🔑 Key Idea

We don’t refuel immediately.

We:

1. Travel as far as possible.
2. Store all reachable stations' fuel in a **max heap**.
3. When we can’t go further → take the largest fuel available.
4. Repeat until target reached.

---

# 💻 Java Code

```java
class Solution {
    public int minRefuelStops(int target, int startFuel, int[][] stations) {

        int max_you_can_reach = startFuel;

        PriorityQueue<Integer> pq =
            new PriorityQueue<>(Collections.reverseOrder());

        int count = 0;
        int index = 0;

        while(max_you_can_reach < target){

            while(index < stations.length &&
                  stations[index][0] <= max_you_can_reach){

                pq.offer(stations[index][1]);
                index++;
            }

            if(pq.isEmpty())
                return -1;

            max_you_can_reach += pq.poll();
            count++;
        }

        return count;
    }
}
```

---

# 🎯 Why Max Heap?

At every step:

We want the **largest fuel among reachable stations**.

Because:

Choosing smaller fuel first may increase number of stops.

Greedy choice:

```
Always take largest available fuel.
```

---

# 🧠 Dry Run

Input:
```
target = 100
startFuel = 10
stations = [[10,60],[20,30],[30,30],[60,40]]
```

Start:
```
Reach = 10
```

Station at 10 reachable → add 60

Take 60:
```
Reach = 70
Stops = 1
```

Now stations at:
20, 30, 60 reachable → add 30, 30, 40

Take 40:
```
Reach = 110
Stops = 2
```

Reached target.

---

# ⏱ Time Complexity

```
O(n log n)
```

- Each station pushed once
- Each poll takes log n

---

# 📦 Space Complexity

```
O(n)
```

For heap.

---

# 🔥 Pattern Used

Greedy  
Max Heap  
Delayed Decision Strategy  

---

# 🧠 Why This Greedy Works?

Because:

If we delay refueling and always pick the largest available fuel,

We minimize number of stops.

This is similar to:

- Jump Game II (greedy range expansion)
- K Closest Points (heap control)

---

# ⚠ Important Insight

We only refuel when necessary.

We do NOT refuel at every station.

That’s the greedy trick.

---

# 🏆 Interview Insight

This is a strong greedy + heap problem.

It tests:

- Decision making
- Heap usage
- Simulation
- Greedy correctness reasoning

---

# ✅ Final Output

Input:
```
target = 100
startFuel = 10
stations = [[10,60],[20,30],[30,30],[60,40]]
```

Output:
```
2
```

