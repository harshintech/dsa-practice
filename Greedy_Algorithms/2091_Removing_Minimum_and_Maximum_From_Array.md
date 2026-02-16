# 🗑 Minimum Deletions to Remove Min & Max

---

## 📌 Problem

Given an integer array `nums`,  
remove the **minimum number of elements** so that:

```
Both the minimum and maximum element are removed.
```

You can delete elements:

- From the front
- From the back

Only those two operations are allowed.

---

## 🧩 Example

Input:
```
nums = [2,10,7,5,4,1,8,6]
```

Minimum element:
```
1 (index 5)
```

Maximum element:
```
10 (index 1)
```

Output:
```
5
```

---

# 🚀 Approach (Greedy + Case Analysis)

---

## 🔑 Step 1: Find Min & Max Index

We store:

```
minIndex
maxIndex
```

---

# 🧠 Possible Deletion Strategies

There are only 3 valid ways:

---

### 🟢 Case 1: Remove from Front Only

Remove up to the farthest index.

```
max(minIndex, maxIndex) + 1
```

---

### 🟢 Case 2: Remove from Back Only

Remove from end up to the smaller index.

```
n - min(minIndex, maxIndex)
```

---

### 🟢 Case 3: Remove From Both Sides

Remove:

- Smaller index from front
- Larger index from back

Formula:

```
(min(minIndex, maxIndex) + 1)
+
(n - max(minIndex, maxIndex))
```

---

# 💻 Java Code

```java
class Solution {
    public int minimumDeletions(int[] nums) {
        
        int maxIndex = 0;
        int minIndex = 0;
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;

        // Step 1: Find min & max index
        for(int i = 0; i < nums.length; i++){
            int n = nums[i];

            if(min > n){
                minIndex = i;
                min = n;
            }

            if(max < n){
                maxIndex = i;
                max = n;
            }
        }

        int n = nums.length;

        // Case 3: both sides
        int case3 =
            Math.min(minIndex, maxIndex) + 1
            +
            (n - Math.max(minIndex, maxIndex));

        // Case 1: only front
        int case1 =
            Math.max(minIndex, maxIndex) + 1;

        // Case 2: only back
        int case2 =
            n - Math.min(minIndex, maxIndex);

        return Math.min(case3,
                Math.min(case1, case2));
    }
}
```

---

# 🧠 Dry Run Example

```
nums = [2,10,7,5,4,1,8,6]
```

minIndex = 5  
maxIndex = 1  
n = 8  

---

### Case 1 (Front only):

```
max(5,1)+1 = 6
```

---

### Case 2 (Back only):

```
8 - min(5,1) = 7
```

---

### Case 3 (Both sides):

```
min(5,1)+1 = 2
+
8 - max(5,1) = 3
Total = 5
```

Answer:
```
5
```

---

# ⏱ Time Complexity

```
O(n)
```

Single traversal.

---

# 📦 Space Complexity

```
O(1)
```

Only variables used.

---

# 🔥 Pattern Used

Greedy  
Index Analysis  
Case Enumeration  

---

# 🧠 Why This Is Smart

Instead of brute force deletion simulation:

We analyze only 3 logical possibilities.

Because:

You can delete only from ends.

---

# 🏆 Interview Insight

Whenever problem says:

```
Delete only from front or back
```

Think:

```
Index-based case analysis
```

---

# ✅ Final Output

Input:
```
[2,10,7,5,4,1,8,6]
```

Output:
```
5
```

---


