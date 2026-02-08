# LeetCode 2226 - Maximum Candies Allocated to K Children

---

## 📌 Problem

You are given:

- `candies[]` → number of candies in each pile  
- `k` → number of children  

You must distribute candies such that:

- Each child gets **exactly same number of candies**
- Candies given to a child must come from **only one pile**
- You can split piles

Return the **maximum number of candies each child can get**.

If not possible → return `0`.

---

## 🧩 Example

Input:
```
candies = [5,8,6]
k = 3
```

Output:
```
5
```

Explanation:

If each child gets 5 candies:

From piles:
```
5 → 1 child
8 → 1 child
6 → 1 child
```

Total children served = 3 ✅

---

# 🚀 Approach (Binary Search on Answer)

## 🔑 Key Idea

We want to maximize:

```
candies per child
```

Search space:

```
1 → max(candies)
```

Why Binary Search?

Because:

- If we can give `x` candies per child,
- Then any smaller value will also work.

This is a **monotonic condition**.

---

# 💻 Java Code

```java
class Solution {
    public int maximumCandies(int[] candies, long k) {

        int low = 1;   
        int high = 0;
        int ans = 0;

        for (int c : candies) {
            high = Math.max(high, c);
        }

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (possible(candies, mid, k)) {
                ans = mid;
                low = mid + 1;   
            } else {
                high = mid - 1;
            }
        }

        return ans;
    }

    public boolean possible(int[] candies, int pile, long k) {

        long count = 0;   // long important

        for (int c : candies) {
            count += c / pile;
        }

        return count >= k;
    }
}
```

---

# 🎨 How possible() Works

If we try giving:

```
pile = 4 candies per child
```

Then from each pile:

```
count += candies[i] / 4
```

Example:

```
candies = [5,8,6]
pile = 4
```

Calculation:

```
5 / 4 = 1
8 / 4 = 2
6 / 4 = 1
Total = 4 children
```

If `k = 3`, then valid.

---

# 🧠 Why We Use long for count?

Because:

```
k can be very large
```

If we use int, overflow may happen.

---

# 🔥 Dry Run Example

Input:
```
candies = [5,8,6]
k = 3
```

Range:
```
1 → 8
```

Try mid = 4  
Possible? Yes (4 children)

Try bigger → mid = 6  
Possible?  
```
5/6 = 0
8/6 = 1
6/6 = 1
Total = 2 ❌
```

Reduce.

Eventually answer becomes:
```
5
```

---

# ⏱ Time Complexity

O(n log m)

Where:

- n = number of piles
- m = maximum candy pile

---

# 📦 Space Complexity

O(1)

---

# 🔥 Pattern Used

Binary Search on Answer  
Greedy Counting  
Monotonic Condition  

---

# ⚠ Important Edge Case

If total candies < k:

```
Answer = 0
```

Because even giving 1 candy per child is impossible.

---

# 🏆 Interview Insight

Whenever problem asks:

> Maximize minimum value satisfying condition

Think:

```
Binary Search on Answer
```

---

# ✅ Final Output

Input:
```
[5,8,6], k = 3
```

Output:
```
5
```

