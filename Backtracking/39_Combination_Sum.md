# 🎯 Combination Sum (Backtracking)

---

## 📌 Problem

Given:

- `candidates[]` → distinct integers  
- `target` → target sum  

Return all **unique combinations** where:

```
Numbers sum to target
```

⚠ Each number can be used **unlimited times**.

---

## 🧩 Example

Input:
```
candidates = [2,3,6,7]
target = 7
```

Output:
```
[
 [2,2,3],
 [7]
]
```

---

# 🚀 Approach (Backtracking)

---

## 🔑 Core Idea

At every index:

We have 2 choices:

1️⃣ Take the current number  
2️⃣ Skip and move forward  

But since we can reuse numbers:

👉 When taking a number,  
we call recursion with **same index (i)**

---

# 💻 Java Code

```java
class Solution {
    public List<List<Integer>> combinationSum(
            int[] candidates, int target) {

        List<List<Integer>> list = new ArrayList<>();

        backtrack(list, new ArrayList<>(),
                  candidates, 0, target);

        return list;
    }

    private void backtrack(
            List<List<Integer>> list,
            List<Integer> tempList,
            int[] candidates,
            int start,
            int target) {

        if (target < 0)
            return;

        if (target == 0) {
            list.add(new ArrayList<>(tempList));
            return;
        }

        for (int i = start;
             i < candidates.length; i++) {

            tempList.add(candidates[i]);

            // Reuse allowed → pass i
            backtrack(list, tempList,
                      candidates, i,
                      target - candidates[i]);

            tempList.remove(tempList.size() - 1);
        }
    }
}
```

---

# 🧠 Why `i` (Not `i + 1`)?

Because:

```
Unlimited usage allowed.
```

If we used `i + 1`:

We would prevent reuse.

---

# 🌳 Decision Tree Example

Input:
```
[2,3,6,7], target = 7
```

Tree (simplified):

```
Start
 |
 2 → target=5
   |
   2 → target=3
     |
     2 → target=1 (stop)
     3 → target=0 ✔
 |
 3 → target=4
   |
   3 → target=1 (stop)
 |
 6 → target=1 (stop)
 |
 7 → target=0 ✔
```

---

# 🧠 Dry Run

For `[2,3]`, target=5:

Start:

```
[]
```

Take 2:
```
[2] → target=3
```

Take 2:
```
[2,2] → target=1
```

Take 3:
```
[2,3] → target=0 ✔
```

Backtrack and try 3:

```
[3] → target=2
```

No solution.

---

# ⏱ Time Complexity

Worst case:

```
O(2^n) (approx exponential)
```

Depends on branching.

---

# 📦 Space Complexity

Recursion depth:
```
O(target)
```

Result storage:
Depends on combinations.

---

# 🔥 Pattern Used

Backtracking  
Target Reduction  
Reuse Allowed  

---

# 🏆 Compare with Other Problems

| Problem | Reuse Allowed? | Skip Duplicates? |
|----------|---------------|-----------------|
| Combination Sum | ✅ Yes | ❌ No duplicates in input |
| Combination Sum II | ❌ No | ✅ Handle duplicates |
| Subsets | ❌ No reuse | ❌ |
| Permutations | ❌ No reuse | ❌ |

---

# ⚠ Important Insight

We reduce target at each recursion:

```
target - candidates[i]
```

When target becomes:

```
0 → valid solution
< 0 → stop branch
```

---

# ✅ Final Output

Input:
```
[2,3,6,7], target=7
```

Output:
```
[[2,2,3],[7]]
```

---

