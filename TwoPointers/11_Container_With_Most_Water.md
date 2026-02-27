# 💧 Container With Most Water

---

## 📌 Problem

You are given an array:

```
height[i]
```

Each value represents a vertical line.

You must choose **two lines** such that they store **maximum water**.

---

## ✅ Code (UNCHANGED)

```java
class Solution {
    public int maxArea(int[] height) {

        int low = 0;
        int high = height.length - 1;
        int maxWater = 0;

        while(low < high){

            int h = Math.min(height[low],height[high]);

            int water = h * (high - low);

            maxWater = Math.max(maxWater,water);

            if(height[low] < height[high]){
                low++;
            }else{
                high--;
            }
        }

        return maxWater;
        
    }
}
```

---

# 🧠 Water Formula

Water stored between two lines:

```
Water = min(height[left], height[right]) × width
```

Where:

```
width = right - left
```

---

# 🎯 Key Observation

Water depends on:

```
✅ smaller height
✅ distance between lines
```

Because water spills from smaller wall.

Example:

```
|       |
|       |
|   |   |
---------
```

Height = smaller wall only.

---

# 🚫 Brute Force Idea

Try all pairs:

```
(i, j)
```

Time Complexity:

```
O(n²)
```

Too slow.

---

# 🚀 Optimal Idea → Two Pointer

Start from **maximum width**.

```
low = 0
high = n-1
```

Why?

Because width is largest initially.

---

# 🔥 MOST IMPORTANT LOGIC

After calculating area:

We move **only the smaller height pointer**.

---

## ❓ Why move smaller height?

Suppose:

```
height[low] < height[high]
```

Current water depends on:

```
height[low]
```

If we move `high`:

```
width ↓
height limit SAME
→ water can only decrease ❌
```

So moving taller wall is useless.

---

✅ Only hope:

Increase smaller height.

So move:

```
low++
```

---

### Rule

```
Move the smaller height pointer
```

---

# 🧠 Visual Intuition

```
low                high
 |                  |
 1   8   6   2   5   4
```

Water limited by:

```
min(1,4) = 1
```

Move smaller → `low++`

Now maybe height increases.

---

# 🔄 Algorithm Flow

```
1. Calculate area
2. Update max
3. Move smaller pointer
4. Repeat
```

---

# 🧩 Dry Run

Input:

```
[1,8,6,2,5,4,8,3,7]
```

Step 1:

```
low=0, high=8
height=1
width=8
area=8
```

Move low.

---

Step 2:

```
low=1, high=8
min(8,7)=7
width=7
area=49 ✅ MAX
```

Continue shrinking.

Final Answer:

```
49
```

---

# ⏱ Complexity

### Time
```
O(n)
```

Each pointer moves once.

### Space
```
O(1)
```

---

# 🏆 Pattern Recognition (Interview Gold)

If problem contains:

```
Two ends
Max / Min area
Distance involved
```

Think immediately:

```
Two Pointer Optimization
```

---

# 🔥 Golden Rule

```
Area limited by smaller height.
So move smaller height pointer.
```

This single idea converts:

```
O(n²) → O(n)
```

---

# 🚀 Level Upgrade Insight

This belongs to:

```
Greedy + Two Pointer Pattern
```

Same thinking used in:

✅ Trapping Rain Water  
✅ Two Sum Sorted  
✅ Boats to Save People  

---
