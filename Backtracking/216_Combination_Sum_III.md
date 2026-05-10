# 🎯 Combination Sum III

---

## 📌 Problem

Find all possible combinations of:

- Exactly `k` numbers
- Numbers are chosen from `1` to `9`
- Each number can be used **only once**
- Sum of chosen numbers must be `n`

---

## ✅ Example

Input:

```text
k = 3
n = 7
```

Output:

```text
[[1,2,4]]
```

Because:

```text
1 + 2 + 4 = 7
```

---

## ✅ Code (UNCHANGED)

```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {

        List<List<Integer>> resultSet = new ArrayList<>();
        backtrack(resultSet, new ArrayList<>(), k, n, 0, 1);
        return resultSet;

    }

    private void backtrack(List<List<Integer>> resultSet, List<Integer> temp, int k, int n, int sum, int start) {

        if (temp.size() == k) {
            if (sum == n) {
                resultSet.add(new ArrayList<>(temp)); // Add a copy!
            }
            return;
        }

        for (int i = start; i < 10; i++) {

            if (sum + i > n)
                break;
    
            temp.add(i);
            backtrack(resultSet, temp, k, n, sum + i, i + 1);
            temp.remove(temp.size() - 1);
        }
    }
}
```

---

# 🧠 Core Idea

This is a classic **Backtracking** problem.

At every step:

1. Choose a number from `start` to `9`
2. Add it to current combination
3. Recurse
4. Remove it (backtrack)

---

# 🎯 Why `i + 1` ?

```java
backtrack(..., sum + i, i + 1);
```

This means:

> Next recursive call starts from the next number.

So if current number is `3`, next choices are:

```text
4, 5, 6, 7, 8, 9
```

---

## ✅ Benefits of `i + 1`

### 1. No Reuse of Same Number
If we choose `3`, we cannot choose `3` again.

### 2. Avoid Duplicate Combinations
We generate:

```text
[1,2,4]
```

but never:

```text
[2,1,4]
[4,1,2]
```

---

# ✂️ Pruning Optimization

```java
if (sum + i > n)
    break;
```

---

## Why `break` Works

Numbers are tried in increasing order:

```text
1, 2, 3, 4, ...
```

If:

```text
sum + i > n
```

Then all larger numbers will also exceed `n`.

So we can stop immediately.

---

## Example

```text
sum = 6
n = 7
```

Try:

```text
i = 2
6 + 2 = 8 > 7
```

Since numbers after 2 are larger, no need to continue.

---

# 🧩 Base Case

```java
if (temp.size() == k)
```

We have selected exactly `k` numbers.

Now:

- If `sum == n` → valid combination
- Otherwise → discard

---

# 🌳 Example Walkthrough

Input:

```text
k = 3
n = 7
```

Path:

```text
[]
 └── 1
      └── 2
           └── 4  → [1,2,4] ✅
```

Because:

```text
1 + 2 + 4 = 7
```

---

# 🔄 Backtracking Flow

```text
Choose number
↓
Recurse
↓
Undo choice
↓
Try next number
```

---

# ⏱ Complexity

Worst case:

```text
O(C(9, k))
```

We choose `k` numbers from 9 possible numbers.

---

# 💾 Space Complexity

```text
O(k)
```

Maximum recursion depth is `k`.

---

# 🏆 Interview Pattern Recognition

If problem asks for:

- All combinations
- Fixed size (`k`)
- Numbers chosen once
- Target sum

Think:

```text
Backtracking + Start Index + Pruning
```

---

# 🔥 Golden Rules

### Use `i + 1`
```text
Each number can be used only once
```

### Use `sum + i`
```text
Track running sum efficiently
```

### Use `break`
```text
Stop early when target exceeded
```
