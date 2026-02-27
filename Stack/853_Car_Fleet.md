# 🚗 Car Fleet

---

## 📌 Problem

You are given:

```
target → destination point
position[i] → starting position of car i
speed[i] → speed of car i
```

Rules:

- Cars move towards target.
- If a faster car catches a slower car, they form a fleet.
- A fleet moves at the slowest speed.
- Return total number of fleets reaching target.

---

## ✅ Code

```java
class Solution {
    public int carFleet(int target, int[] position, int[] speed) {
        int n = position.length;

        int[][] cars = new int[n][2];
        for(int i = 0;i<n;i++){
            cars[i][0] = position[i];
            cars[i][1] = speed[i];
        }

        Arrays.sort(cars,(a,b) -> Integer.compare(b[0],a[0]));

        Stack<Double> st = new Stack<>();

        for(int []car : cars){
            int pos = car[0];
            int spd = car[1];
            double timeTaken = (double)(target - pos) / spd;

            if(st.isEmpty() || timeTaken > st.peek()){
                st.push(timeTaken);
            }
        }

         return st.size();
    }

}
```

---

# 🧠 Core Idea

Instead of simulating movement,

we calculate:

```
Time each car takes to reach target
```

Formula:

```
time = (target - position) / speed
```

---

# 🎯 Why Sort by Position (Descending)?

We sort from **closest to target → farthest**.

Why?

Because:

```
A car behind can catch a car in front.
But front car cannot affect cars ahead.
```

So we process from front to back.

---

# 🔥 Key Observation

If a car behind reaches earlier than front car:

```
It will catch up → become same fleet
```

If it reaches later:

```
It cannot catch up → new fleet
```

---

# 🧩 Stack Meaning

Stack stores:

```
Time of fleets
```

---

# 🚀 Logic Explanation

For each car:

### Case 1:
```
timeTaken > topTime
```

Car arrives later → cannot catch previous fleet.

→ New fleet → push.

---

### Case 2:
```
timeTaken <= topTime
```

Car arrives earlier or same time → will catch previous fleet.

→ Do NOT push.

It merges automatically.

---

# 📊 Example

Input:

```
target = 12
position = [10,8,0,5,3]
speed =    [2,4,1,1,3]
```

After sorting (descending position):

```
[10,2]
[8,4]
[5,1]
[3,3]
[0,1]
```

---

### Calculate Time

Car 1:
```
(12-10)/2 = 1
```
Stack = [1]

---

Car 2:
```
(12-8)/4 = 1
```
1 <= 1 → merges
Stack = [1]

---

Car 3:
```
(12-5)/1 = 7
```
7 > 1 → new fleet
Stack = [1,7]

---

Car 4:
```
(12-3)/3 = 3
```
3 <= 7 → merges
Stack = [1,7]

---

Car 5:
```
(12-0)/1 = 12
```
12 > 7 → new fleet
Stack = [1,7,12]

---

Final fleets:

```
3
```

---

# 🧠 Why This Works (Important Insight)

Once a fleet forms,

its arrival time becomes fixed.

Any car behind:

```
If reaches earlier → merges
If reaches later → new fleet
```

So stack stores increasing arrival times.

---

# ⏱ Complexity

### Sorting
```
O(n log n)
```

### Stack pass
```
O(n)
```

Total:
```
O(n log n)
```

---

# 💾 Space Complexity

```
O(n)
```

For stack.

---

# 🏆 Pattern Recognition

If problem contains:

```
Objects moving
Catching up
Merging
Arrival time comparison
```

Think:

```
Sort + Stack + Time comparison
```

---

# 🔥 Golden Rule

```
Process from closest to target.
If new car time > previous fleet time → new fleet.
Else merge.
```

---

# 🚀 Interview Level Insight

This is a:

```
Monotonic Stack pattern (increasing times)
```

Similar thinking used in:

✅ Daily Temperatures  
✅ Next Greater Element  
✅ Largest Rectangle  

---

