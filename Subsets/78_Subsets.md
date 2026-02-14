# LeetCode 78 - Subsets (Backtracking)

---

## 📌 Problem

Given an integer array `nums`,  
return **all possible subsets** (the power set).

The solution set must not contain duplicate subsets.

---

## 🧩 Example

Input:
```
nums = [1,2,3]
```

Output:
```
[
 [],
 [1],
 [1,2],
 [1,2,3],
 [1,3],
 [2],
 [2,3],
 [3]
]
```

---

# 🚀 Approach (Backtracking)

---

## 🔑 Core Idea

At each index, we have 2 choices:

```
1️⃣ Include the element
2️⃣ Exclude the element
```

This naturally forms a **decision tree**.

---

# 🌳 Decision Tree Visualization

For `[1,2,3]`:

```
                 []
              /        \
            1            -
         /     \      
       2         -     
     /   \      
   3       -
```

Every node represents a subset.

---

# 💻 Java Code

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {

        List<List<Integer>> resultSets = new ArrayList<>();

        backtrack(resultSets, new ArrayList<>(), nums, 0);

        return resultSets;
    }

    public void backtrack(
            List<List<Integer>> resultSets,
            List<Integer> tempSets,
            int[] nums,
            int start){

        // Add current subset (very important)
        resultSets.add(new ArrayList<>(tempSets));

        for(int i = start; i < nums.length; i++){

            tempSets.add(nums[i]);

            backtrack(resultSets, tempSets, nums, i + 1);

            // Backtrack (undo choice)
            tempSets.remove(tempSets.size() - 1);
        }
    }
}
```

---

# 🎯 Why `new ArrayList<>(tempSets)`?

Because:

```
Lists are stored by reference.
```

If we directly add `tempSets`,  
all subsets will point to the same list.

So we create a **copy**.

---

# 🧠 Dry Run

Input:
```
[1,2]
```

Steps:

Start:
```
[]
```

Include 1:
```
[1]
```

Include 2:
```
[1,2]
```

Backtrack:
```
[1]
```

Backtrack:
```
[]
```

Include 2:
```
[2]
```

Final:
```
[], [1], [1,2], [2]
```

---

# ⏱ Time Complexity

Total subsets:

```
2^n
```

Each subset copy takes O(n)

So total:

```
O(n × 2^n)
```

---

# 📦 Space Complexity

Recursion stack:

```
O(n)
```

Result storage:

```
O(n × 2^n)
```

---

# 🔥 Pattern Used

Backtracking  
Decision Tree  
Include / Exclude Strategy  

---

# 🏆 Interview Insight

This is the foundation of:

- Subsets II
- Combination Sum
- Permutations
- N-Queens
- Sudoku Solver

If you master this template,
you master backtracking.

---

# ✅ Final Output

Input:
```
[1,2,3]
```

Output:
```
All 8 subsets
```

---

