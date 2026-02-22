# 🔺 132 Pattern (Leetcode 456)

---

## 📌 Problem

Given an array:

```
nums[]
```

Find whether there exists a pattern:

```
nums[i] < nums[k] < nums[j]
```

such that:

```
i < j < k
```

This is called **132 Pattern**.

---

## 🎯 Pattern Meaning

We need:

```
1   3   2
i < j < k
```

Example:

```
nums = [3,1,4,2]
```

Valid pattern:

```
1 4 2
↑ ↑ ↑
i j k
```

Because:

```
1 < 2 < 4
```

✅ Answer = true

---

---

# ✅ Approach 1 — Ordered Set (TreeSet)

---

## 🧠 Idea

We fix:

```
j → middle element (3)
```

Then search:

```
left side → minimum value (1)
right side → value between them (2)
```

---

### Step 1
Create:

```
leftMin[i]
```

which stores minimum element from left.

---

### Step 2
Traverse from right side.

Use:

```
TreeSet
```

to find number:

```
greater than leftMin[j]
but smaller than nums[j]
```

---

## 💻 Code  (Ordered Set - Not Recommanded ❌) 

```java
import java.util.*;

class Solution {
    public boolean find132pattern(int[] nums) {
        int n = nums.length;
        if (n < 3) return false;

        int[] leftMin = new int[n];
        leftMin[0] = nums[0];

        // Step 1: Build leftMin array
        for (int i = 1; i < n; i++) {
            leftMin[i] = Math.min(leftMin[i - 1], nums[i]);
        }

        TreeSet<Integer> set = new TreeSet<>();

        // Step 2: Traverse from right
        for (int j = n - 1; j >= 0; j--) {

            if (nums[j] > leftMin[j]) {

                // find number greater than leftMin[j]
                Integer k = set.higher(leftMin[j]);

                if (k != null && k < nums[j]) {
                    return true;
                }
            }

            set.add(nums[j]);
        }

        return false;
    }
}
```

---

## ⏱ Complexity

```
Time  : O(N log N)
Space : O(N)
```

(TreeSet operations)

---

---

# ✅ Approach 2 — MONOTONIC STACK ⭐ (Optimal)

🔥 This is the **interview favorite solution**

---

## 🧠 Genius Observation

Instead of searching all triples:

We scan **from RIGHT → LEFT**.

Why?

Because:

```
k must be after j
```

So right traversal helps.

---

## 🔥 Key Variables

```
stack → decreasing numbers (possible nums[j])
third → represents nums[k]
```

Meaning:

```
third = best candidate for '2'
```

---

## ⚡ Algorithm Logic

---

### Traverse from right

For each element:

---

### ✅ Case 1

```
nums[i] < third
```

We found:

```
1 < 2 < 3
```

Pattern exists ✅

---

### ✅ Case 2

Maintain decreasing stack

```
while nums[i] > stack.top()
```

Pop elements and update:

```
third = popped value
```

Why?

Because popped value becomes valid `nums[k]`.

---

### ✅ Push current element

Possible future `nums[j]`.

---

## 💻 Code

```java
class Solution {
    public boolean find132pattern(int[] nums) {
        int n = nums.length;
        if (n < 3) return false;

        // Stack<Integer> stack = new Stack<>();
        Deque<Integer> stack = new ArrayDeque<>();
        int third = Integer.MIN_VALUE; // this will act as nums[k]

        for(int i = n - 1;i>=0;i--){

            // If current element is less than third,
            // we found nums[i] < nums[k]
            if(nums[i] < third){
                return true;
            }

            // Maintain decreasing stack
            while(!stack.isEmpty() && nums[i] > stack.peek()){
                third = stack.pop();
            }

            stack.push(nums[i]);
        }

        return false;
    }
}
```

---

## 🌊 Visualization

Example:

```
nums = [3,1,4,2]
```

Traverse backward:

```
Start from right
```

Stack Process:

```
2 → push
4 → pop 2 → third=2
1 → 1 < 2 ✅ FOUND
```

Pattern exists.

---

## ⏱ Complexity

```
Time  : O(N)
Space : O(N)
```

🔥 Optimal solution.

---

---

# 🧩 Comparison

| Approach | Time | Difficulty |
|---|---|---|
| TreeSet | O(N log N) | Medium |
| Monotonic Stack | ⭐ O(N) | Hard / Interview |

---

---

# 🔥 Pattern Recognition

If problem involves:

```
132 / 231 / next smaller
future constraint
right-side dependency
```

👉 Think:

```
Monotonic Stack
```

---

# 🏆 Golden Interview Insight

```
Scan from RIGHT
+
Maintain decreasing stack
+
Track middle element
```

= 132 Pattern Solution

---


