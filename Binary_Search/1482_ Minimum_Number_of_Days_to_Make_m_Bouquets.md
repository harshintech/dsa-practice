# LeetCode 1482 - 🌸 Minimum Number of Days to Make m Bouquets

---

## 📌 Problem

You are given:

- `bloomDay[]` → the day each flower blooms
- `m` → number of bouquets needed
- `k` → number of adjacent flowers required for 1 bouquet

Return the **minimum number of days** required to make `m` bouquets.

If impossible → return `-1`.

---

## 🧩 Example

Input:
```
bloomDay = [1,10,3,10,2]
m = 3
k = 1
```

Output:
```
3
```

---

# 🚀 Approach (Binary Search on Answer)

## 🔑 Key Idea

We search for minimum `day` such that:

```
We can make at least m bouquets
```

Range of answer:

```
min(bloomDay) → max(bloomDay)
```

Why Binary Search?

Because:

- If it's possible on day X,
- It will also be possible on any day > X.

This is a **monotonic condition**.

---

# 💻 Java Code

```java
class Solution {

    public int minDays(int[] bloomDay, int m, int k) {

        long need = (long) m * k;

        if (need > bloomDay.length)
            return -1;

        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;

        for (int d : bloomDay) {
            min = Math.min(min, d);
            max = Math.max(max, d);
        }

        int low = min;
        int high = max;
        int ans = -1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (possibleDay(bloomDay, m, k, mid)) {
                ans = mid;
                high = mid - 1;   // try smaller day
            } else {
                low = mid + 1;    // need more days
            }
        }

        return ans;
    }

    private boolean possibleDay(int[] bloomDay, int m, int k, int day){

        int flower = 0;
        int count = 0;

        for(int i = 0; i < bloomDay.length; i++){

            if(bloomDay[i] <= day){
                flower++;
            } else {
                count += flower / k;
                flower = 0;
            }
        }

        count += flower / k;

        return count >= m;
    }
}
```

---

# 🎨 How possibleDay Works

We simulate:

“If today is `day`, how many bouquets can we make?”

Logic:

```
If bloomDay[i] <= day → flower is bloomed
Else → reset consecutive counter
```

When consecutive flowers reach `k`:

```
count++
```

---

# ⚠️ Important Confusing Point

## ❓ What if `mid` day is NOT in array?

Example:

Range:
```
7 → 12
```

Binary search may try:
```
mid = 9
```

But 9 is not inside array.

Is that wrong?

👉 **NO.**

Because we are asking:

> “If today is day 9, how many flowers have bloomed?”

Condition used:
```
bloomDay[i] <= day
```

We simulate the garden state.

---

## 🔥 Critical Insight

Garden state only changes when:

```
day == bloomDay[i]
```

So final answer will ALWAYS be one of the array values.

Binary search may test:
```
8, 9, 10
```

But first `true` will occur at an actual bloom day.

---

# 🧠 Dry Run Example

```
bloomDay = [1,10,3,10,2]
m = 3
k = 1
```

Range:
```
1 → 10
```

Mid = 5

Flowers bloomed:
```
1,3,2
```

We can make 3 bouquets → valid.

Try smaller.

Eventually answer becomes:
```
3
```

---

# ⏱ Time Complexity

O(n log d)

Where:

- n = number of flowers
- d = max bloom day

Binary search runs log(d) times.

---

# 📦 Space Complexity

O(1)

---

# 🔥 Pattern Used

Binary Search on Answer  
Greedy Counting  
Monotonic Condition  

---

# 🏆 Interview Insight

Whenever problem asks:

> Find minimum day / speed / capacity to satisfy condition

Think:

```
Binary Search on Answer
```

---

# ✅ Final Output

Input:
```
[1,10,3,10,2], m=3, k=1
```

Output:
```
3
```

