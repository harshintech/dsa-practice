# LeetCode 209 - Minimum Size Subarray Sum

---

## 📌 Problem

Given an array of positive integers `nums` and a positive integer `target`,  
return the minimal length of a contiguous subarray whose sum is greater than or equal to `target`.

If there is no such subarray, return `0`.

---

## 🧩 Example

Input:
```
target = 7
nums = [2,3,1,2,4,3]
```

Output:
```
2
```

Explanation:
Subarray `[4,3]` has sum = 7 and length = 2.

---

# 🚀 Approach (Sliding Window)

### 🔑 Key Idea

Since all numbers are **positive**, we can:

- Expand window when sum < target
- Shrink window when sum ≥ target

This guarantees optimal solution in linear time.

---

# 💡 Algorithm Steps

1. Initialize:
   - `start = 0`
   - `sum = 0`
   - `minLen = Integer.MAX_VALUE`
2. Expand window by moving `end`
3. Add `nums[end]` to sum
4. While `sum >= target`:
   - Update minimum length
   - Remove `nums[start]`
   - Move `start`
5. If no valid subarray found → return 0

---

# 💻 Java Code

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {

        int start = 0;
        int end = 0;
        int sum = 0;
        int minLen = Integer.MAX_VALUE;

        while (end < nums.length) {

            sum += nums[end];

            while (sum >= target) {
                minLen = Math.min(minLen, end - start + 1);
                sum = sum - nums[start];
                start++;
            }

            end++;
        }

        return minLen == Integer.MAX_VALUE ? 0 : minLen;
    }
}
```

---

# 🎨 Graphical Representation

Example:

```
target = 7
nums = [2,3,1,2,4,3]
```

---

### Step 1

Window:
```
[2]
sum = 2
```
Not enough → expand.

---

### Step 2

```
[2,3]
sum = 5
```
Not enough → expand.

---

### Step 3

```
[2,3,1]
sum = 6
```
Not enough → expand.

---

### Step 4

```
[2,3,1,2]
sum = 8
```

Now sum ≥ 7 ✅

Length = 4  
Shrink window.

Remove 2:

```
[3,1,2]
sum = 6
```

Stop shrinking.

---

### Step 5

Expand:

```
[3,1,2,4]
sum = 10
```

Shrink:

```
[1,2,4]
sum = 7
length = 3
```

Shrink again:

```
[2,4]
sum = 6
```

---

### Step 6

Expand:

```
[2,4,3]
sum = 9
```

Shrink:

```
[4,3]
sum = 7
length = 2 ✅ (minimum)
```

---

# 🎉 Final Answer

Minimum Length = **2**

---

# ⏱ Time Complexity

O(n)

- Each element visited at most twice.
- Once by `end`
- Once by `start`

---

# 📦 Space Complexity

O(1)

- No extra data structure used.

---

# 🧠 Why This Works

Because all numbers are positive:

- Expanding increases sum
- Shrinking decreases sum

So we never miss a valid window.

---

# 🔥 Pattern Used

Sliding Window  
Two Pointers  
Variable Size Window

---

# ✅ Final Output

Input:
```
target = 7
nums = [2,3,1,2,4,3]
```

Output:
```
2
```

