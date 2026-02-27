# 🔥 Longest Consecutive Sequence

---

## 📌 Problem

Given an unsorted array:

```
nums = [100, 4, 200, 1, 3, 2]
```

Find the length of the **longest consecutive elements sequence**.

Output:

```
4
```

Because:

```
1, 2, 3, 4
```

---

## ✅ Code 

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums.length == 0){
            return 0;
        }

        Set<Integer> set = new HashSet<>();

        for (int num : nums) {
            set.add(num);
        }

        int longest = 0;
        for (int num : set) {
            if (!set.contains(num - 1)) {
                
                int length = 1;

                while (set.contains(num + length)) {
                    length++;
                }

                longest = Math.max(longest, length);
            }
        }

        return longest;

    }
}
```

---

# 🧠 Core Idea

Instead of sorting:

```
O(n log n)
```

We use **HashSet for O(1) lookup**.

---

# 🎯 Key Trick (Most Important)

We only start counting when:

```
num - 1 does NOT exist
```

Meaning:

👉 `num` is the **start of a sequence**

---

# 🔥 Why This Is Genius

Example:

```
nums = [1, 2, 3, 4]
```

Without the condition:

We would check sequence starting from:

```
1 → checks 2,3,4
2 → checks 3,4
3 → checks 4
4 → checks none
```

That becomes:

```
O(n^2)
```

---

But with this condition:

```
if (!set.contains(num - 1))
```

We only start from the **first number of sequence**.

For above example:

```
1 → start (0 not in set)
2 → skip (1 exists)
3 → skip (2 exists)
4 → skip (3 exists)
```

Only 1 start point ✅

So total work = O(n)

---

# 🧩 How Sequence Expands

Once we detect start:

```
length = 1
```

We check:

```
num+1
num+2
num+3
...
```

Until sequence breaks.

---

# 🧠 Mental Visualization

For each number:

```
Is this a sequence starter?
    YES → expand forward
    NO  → skip
```

---

# ⚡ Why Time Complexity Is O(n)

Even though we use a while loop:

Each number is visited at most:

```
1 time in expansion
```

No number is expanded twice.

So total operations:

```
O(n)
```

---

# ⏱ Complexity

### Time
```
O(n)
```

### Space
```
O(n)
```

For HashSet.

---

# 🏆 Interview Pattern Recognition

If problem says:

```
Unsorted array
Consecutive sequence
O(n) time required
```

Immediately think:

```
HashSet + sequence starter trick
```

---

# 🔥 Golden Rule

```
Start only when num - 1 does NOT exist
```

That is the entire optimization.

---

# 🧠 Example Dry Visualization

Input:

```
[100, 4, 200, 1, 3, 2]
```

Set:

```
{100,4,200,1,3,2}
```

Check:

```
100 → 99 not exist → start → length = 1
4   → 3 exists → skip
200 → 199 not exist → start → length = 1
1   → 0 not exist → start → expands 2,3,4 → length = 4
3   → skip
2   → skip
```

Longest = 4

---

# 🚀 Advanced Insight

This is a classic example of:

```
Using hashing to simulate sorting logic
```

Without actually sorting.

---


