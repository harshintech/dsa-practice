# LeetCode 1011 - Capacity To Ship Packages Within D Days

---

## 📌 Problem

You are given:

- `weights[]` → weight of packages (must ship in order)
- `days` → number of days allowed

Each day:

- You load packages in order.
- Total weight per day cannot exceed ship capacity.

Return the **minimum ship capacity** needed to ship all packages within `days`.

---

## 🧩 Example

Input:
```
weights = [1,2,3,4,5,6,7,8,9,10]
days = 5
```

Output:
```
15
```

---

# 🚀 Approach (Binary Search on Answer)

## 🔑 Key Idea

We are searching for the minimum ship capacity.

Capacity must be between:

```
Minimum = max(weights)
Maximum = sum(weights)
```

Why?

- Capacity cannot be less than the heaviest package.
- Capacity cannot be more than total weight.

This is a **Binary Search on Answer** problem.

---

# 💻 Java Code

```java
class Solution {
    public int shipWithinDays(int[] weights, int days) {

        int minCap = 0;
        int maxCap = 0;

        for(int weight : weights){
            minCap = Math.max(minCap, weight);
            maxCap += weight;
        }

        while(minCap < maxCap){

            int mid = minCap + (maxCap - minCap) / 2;

            int D = 1;     // start with 1 day
            int sum = 0;

            for(int weight : weights){

                if(sum + weight > mid){
                    D++;          // need extra day
                    sum = 0;
                }

                sum += weight;
            }

            if(D > days){
                minCap = mid + 1;   // capacity too small
            } else {
                maxCap = mid;       // try smaller capacity
            }
        }

        return minCap;
    }
}
```

---

# 🎨 Step-by-Step Dry Run

Input:
```
weights = [1,2,3,4,5,6,7,8,9,10]
days = 5
```

Range:
```
10 → 55
```

Try mid = 32

Can ship in 2 days → valid  
Try smaller.

Try mid = 15

Day 1: 1+2+3+4+5 = 15  
Day 2: 6+7 = 13  
Day 3: 8  
Day 4: 9  
Day 5: 10  

Exactly 5 days → valid.

Try smaller.

Eventually answer = 15.

---

# 🧠 Why While(minCap < maxCap)?

We are searching for **minimum valid capacity**.

This version of binary search:

- Keeps narrowing toward smallest valid answer.
- Returns `minCap` when both meet.

---

# ⏱ Time Complexity

O(n log S)

Where:

- n = number of packages
- S = sum of weights

---

# 📦 Space Complexity

O(1)

---

# 🔥 Pattern Used

Binary Search on Answer  
Greedy Simulation  
Monotonic Condition  

---

# ⚠ Important Observation

If capacity works for `mid`:

It will also work for any value > mid.

That’s why binary search works.

---

# 🏆 Interview Insight

This problem is same pattern as:

- Koko Eating Bananas  
- Minimum Days to Make Bouquets  
- Split Array Largest Sum  

All are:

```
Binary Search on Answer + Simulation Check
```

---

# ✅ Final Output

Input:
```
[1,2,3,4,5,6,7,8,9,10], days = 5
```

Output:
```
15
```

