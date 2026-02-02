# LeetCode 904 - Fruit Into Baskets

---

## 📌 Problem

You are given an integer array `fruits` where:

- Each element represents a type of fruit.
- You have **2 baskets**.
- Each basket can hold only **one type** of fruit.
- You must pick fruits in a contiguous subarray.

Return the **maximum number of fruits** you can collect.

---

## 🧩 Example

Input:
```
fruits = [1,2,1]
```

Output:
```
3
```

---

Input:
```
fruits = [1,2,3,2,2]
```

Output:
```
4
```

Explanation:
Subarray `[2,3,2,2]` has only 2 types.

---

# 🚀 Approach (Sliding Window + HashMap)

### 🔑 Key Idea

We need the **longest subarray with at most 2 distinct numbers**.

So we:

- Use a sliding window.
- Store fruit counts in a HashMap.
- If distinct fruits > 2 → shrink window.
- Track maximum window length.

---

# 💡 Algorithm Steps

1. Create a `HashMap` to store fruit counts.
2. Expand window using `end`.
3. Add fruit to map.
4. If map size > 2:
   - Remove fruits from left side.
   - Decrease count.
   - Remove if count becomes 0.
5. Update max length.

---

# 💻 Java Code

```java
class Solution {
    public int totalFruit(int[] fruits) {
        
        Map<Integer,Integer> map = new HashMap<>();
        int start = 0;
        int end = 0;

        int len = 0;

        while(end < fruits.length){

            int f = fruits[end];

            map.put(f, map.getOrDefault(f,0) + 1);

            while(map.size() > 2){
                int left = fruits[start];
                map.put(left, map.get(left) - 1);

                if(map.get(left) == 0){
                    map.remove(left);
                }
                start++;
            }

            len = Math.max(len, end - start + 1);
            end++;
        }

        return len;
    }
}
```

---

# 🎨 Graphical Representation

Example:

```
fruits = [1,2,3,2,2]
```

---

### Step 1

Window:
```
[1]
Map = {1:1}
```

---

### Step 2

```
[1,2]
Map = {1:1, 2:1}
```

---

### Step 3

```
[1,2,3]
Map = {1:1, 2:1, 3:1}
```

Now map size = 3 ❌

Shrink window:

Remove 1

```
[2,3]
Map = {2:1, 3:1}
```

---

### Step 4

Expand:

```
[2,3,2]
Map = {2:2, 3:1}
```

---

### Step 5

Expand:

```
[2,3,2,2]
Map = {2:3, 3:1}
```

Length = 4 ✅

---

# 🎉 Final Answer

Maximum fruits collected = **4**

---

# ⏱ Time Complexity

O(n)

- Each element enters window once.
- Each element leaves window once.

---

# 📦 Space Complexity

O(1)

- At most 3 keys in map (constant size).

---

# 🧠 Why This Works

This is the classic:

Longest Subarray with At Most K Distinct Elements

Here K = 2.

Sliding window ensures we always maintain valid condition.

---

# 🔥 Pattern Used

Sliding Window  
HashMap  
At Most K Distinct  

---

# ✅ Final Output

Input:
```
[1,2,3,2,2]
```

Output:
```
4
```

