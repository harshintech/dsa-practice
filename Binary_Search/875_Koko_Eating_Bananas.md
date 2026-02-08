# 🧠 Koko Eating Bananas

---

## 📌 Problem

Koko loves to eat bananas.

You are given:

- `piles[]` → number of bananas in each pile
- `h` → total hours available

Koko eats at a constant speed `k` bananas per hour.

Return the **minimum integer speed `k`** such that she can finish all bananas within `h` hours.

---

## 🧩 Example

Input:
```
piles = [3,6,7,11]
h = 8
```

Output:
```
4
```

---

# 🚀 Approach (Binary Search on Answer)

## 🔑 Key Idea

The eating speed must be between:

```
Minimum speed = 1
Maximum speed = max(piles)
```

We apply **Binary Search** on speed.

Why?

Because:

- If a speed works (can finish in ≤ h hours),
- Then any larger speed will also work.

This is a **monotonic condition**.

---

# 🧠 Helper Function

To check if Koko can finish with speed `k`:

For each pile:

```
hours += ceil(pile / k)
```

If total hours ≤ h → valid speed.

---

# 💻 Java Code

```java
class Solution {

    private boolean canEatTime(int[] piles, int h, int speed){
        long hours = 0;

        for(int pile : piles){
            hours += (long) Math.ceil((double) pile / speed);
            // OR optimized version:
            // hours += (pile + speed - 1) / speed;
        }

        return hours <= h;
    }

    public int minEatingSpeed(int[] piles, int h) {

        int minSpeed = 1;
        int maxSpeed = 0;

        for(int pile : piles){
            maxSpeed = Math.max(maxSpeed, pile);
        }

        int ans = -1;

        while(minSpeed <= maxSpeed){

            int mid = minSpeed + (maxSpeed - minSpeed) / 2;

            if(canEatTime(piles, h, mid)){
                ans = mid;
                maxSpeed = mid - 1;  // try smaller speed
            } else {
                minSpeed = mid + 1;  // increase speed
            }
        }

        return ans;
    }
}
```

---

# 🎨 Step-by-Step Dry Run

Input:
```
piles = [3,6,7,11]
h = 8
```

Range:
```
1 → 11
```

---

### Step 1

Mid = 6

Hours needed:
```
ceil(3/6) = 1
ceil(6/6) = 1
ceil(7/6) = 2
ceil(11/6) = 2
Total = 6 hours
```

Valid (≤ 8)

Save answer = 6  
Try smaller → range = [1,5]

---

### Step 2

Mid = 3

Hours needed:
```
1 + 2 + 3 + 4 = 10 hours
```

Not valid.

Increase speed → range = [4,5]

---

### Step 3

Mid = 4

Hours:
```
1 + 2 + 2 + 3 = 8 hours
```

Valid.

Save answer = 4  
Try smaller → range = [4,3] stop.

---

# 🎉 Final Answer

```
4
```

---

# ⏱ Time Complexity

O(n log m)

Where:
- n = number of piles
- m = max pile size

Binary search runs log(m) times.

---

# 📦 Space Complexity

O(1)

Only variables used.

---

# 🔥 Pattern Used

Binary Search on Answer  
Greedy Checking  
Ceiling Division  

---

# ⚡ Important Optimization

Instead of:

```
Math.ceil((double) pile / speed)
```

Use:

```
(pile + speed - 1) / speed
```

Because:

- Faster
- No floating point

---

# 🏆 Interview Insight

Whenever problem asks:

> Find minimum/maximum value satisfying a condition

Think:

```
Binary Search on Answer
```

---

# ✅ Final Output

Input:
```
[3,6,7,11], h = 8
```

Output:
```
4
```

