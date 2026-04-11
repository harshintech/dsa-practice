# 🔺 Pascal Triangle (Clean Recursive Version)

---

## 📌 Problem

Generate Pascal Triangle up to:

```
numRows
```

---

## ✅ Code (UNCHANGED)

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> result = new ArrayList<>();
        if (numRows == 0) {
            return result;
        }

        if (numRows == 1) {
            List<Integer> firstRow = new ArrayList<>();
            firstRow.add(1);
            result.add(firstRow);
            return result;
        }

        result = generate(numRows - 1);
        List<Integer> prevRow = result.get(numRows - 2);
        List<Integer> currentRow = new ArrayList<>();
        currentRow.add(1);

        for (int i = 1; i < numRows - 1; i++) {
            currentRow.add(prevRow.get(i - 1) + prevRow.get(i));
        }

        currentRow.add(1);
        result.add(currentRow);

        return result;
    }
}
```

---

# 🧠 Core Idea

Each row is built using:

```
previous row
```

Rule:

```
current[i] = prev[i-1] + prev[i]
```

---

# 🔥 Key Improvement in This Version

Instead of:

```
newRow filled with all 1s first ❌
then updating values
```

We directly:

```
build row step by step ✅
```

Cleaner + better readability.

---

# 🧩 Step-by-Step Logic

---

## ✅ Base Case

```
numRows = 1
→ return [[1]]
```

---

## 🔄 Recursive Call

```
result = generate(numRows - 1)
```

Now:

```
result already contains (numRows - 1) rows
```

---

## 🔥 Important Line

```java
List<Integer> prevRow = result.get(numRows - 2);
```

### Why `numRows - 2` ?

Because:

```
Total rows = numRows - 1
Last index = (numRows - 1) - 1 = numRows - 2
```

---

## 🎯 Example

```
numRows = 5
```

```
result = generate(4)
```

```
[
 [1],
 [1,1],
 [1,2,1],
 [1,3,3,1]  ← prevRow
]
```

Index:

```
4 - 1 = 3 → numRows - 2 = 3
```

---

# 🏗 Building Current Row

---

## Step 1

```java
currentRow.add(1);
```

Start:

```
[1]
```

---

## Step 2 (Middle values)

```java
prev[i-1] + prev[i]
```

Example:

```
prev = [1,3,3,1]
```

```
1+3 = 4
3+3 = 6
3+1 = 4
```

---

## Step 3

```java
currentRow.add(1);
```

Final row:

```
[1,4,6,4,1]
```

---

# 🧠 Full Recursion Flow

```
generate(5)
  → generate(4)
      → generate(3)
          → generate(2)
              → generate(1)
```

Then builds:

```
[1]
[1,1]
[1,2,1]
[1,3,3,1]
[1,4,6,4,1]
```

---

# ⏱ Complexity

### Time
```
O(n²)
```

Total elements in triangle.

---

### Space
```
O(n²)
```

Result + recursion stack.

---

# 🏆 Interview Insight

This version is better because:

✅ Cleaner logic  
✅ No unnecessary overwriting  
✅ Easier to explain  

---

# 🔥 Golden Understanding

```
Each row depends ONLY on previous row
```

That’s why recursion works perfectly.

---

# 🚀 Pattern Recognition

This is:

```
Recursion + Building from previous result
```

Same idea used in:

✅ DP problems  
✅ Fibonacci variations  
✅ Triangle DP  

---
