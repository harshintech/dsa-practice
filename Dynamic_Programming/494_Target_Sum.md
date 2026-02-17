# 🎯 Target Sum (Convert to Subset Sum Count)

---

## 📌 Problem

You are given:

```
nums[]  → array of integers
target  → target value
```

Each number can have:

```
+ sign OR - sign
```

Return the **number of ways** to assign signs so that:

```
Total sum = target
```

---

## 🧩 Example

Input:
```
nums = [1,1,1,1,1]
target = 3
```

Output:
```
5
```

Example valid expression:
```
+1 +1 +1 -1 +1 = 3
```

---

# 🚀 Core Mathematical Idea

---

## 🔑 Step 1: Split Into Two Groups

Assume:

```
P → Positive group
N → Negative group
```

Then:

```
sum(P) - sum(N) = target
```

We also know:

```
sum(P) + sum(N) = totalSum
```

---

## 🔑 Step 2: Add Both Equations

```
(sum(P) - sum(N))
+
(sum(P) + sum(N))
=
target + totalSum
```

Cancel `sum(N)`:

```
2 * sum(P) = target + totalSum
```

So:

```
sum(P) = (target + totalSum) / 2
```

---

# 🎯 Final Conversion

Problem becomes:

```
Count subsets with sum = (target + totalSum) / 2
```

This is:

```
Count Subset Sum Problem
```

---

# ⚠ Important Conditions

If:

```
(target + totalSum) is odd
OR
|target| > totalSum
```

Then:

```
Return 0
```

Because it's impossible.

---

# 💻 Java Code

```java
class Solution {

    public int findTargetSumWays(int[] nums, int target) {

        int totalSum = 0;

        for (int num : nums) {
            totalSum += num;
        }

        // If not possible
        if ((target + totalSum) % 2 != 0 ||
            Math.abs(target) > totalSum) {
            return 0;
        }

        int subsetSum =
            (target + totalSum) / 2;

        int[] dp =
            new int[subsetSum + 1];

        dp[0] = 1;   // 1 way to make sum 0

        for (int num : nums) {

            for (int j = subsetSum;
                 j >= num; j--) {

                dp[j] += dp[j - num];
            }
        }

        return dp[subsetSum];
    }
}
```

---

# 🧠 Why Backward Loop?

```
for (j = subsetSum → num)
```

Because:

This is **0/1 Knapsack counting**

Each number can be used only once.

---

# 🧠 Dry Run

Input:
```
nums = [1,1,1,1,1]
target = 3
```

totalSum = 5  

```
subsetSum = (3 + 5) / 2 = 4
```

Now count subsets with sum = 4.

Possible subsets:

Choose any 4 ones.

Number of ways:

```
5C4 = 5
```

Answer:
```
5
```

---

# ⏱ Time Complexity

```
O(n × subsetSum)
```

---

# 📦 Space Complexity

```
O(subsetSum)
```

---

# 🔥 Pattern Used

0/1 Knapsack (Counting Version)  
Subset Sum Transformation  
Mathematical Reduction  

---

# 🏆 Why This Problem Is Important

This is one of the most important DP transformations.

Whenever you see:

```
+ / - assignment
```

Think:

```
Convert to subset sum
```

---

# 🧠 Related Problems

- Partition Equal Subset Sum
- Count Subsets with Given Sum
- Minimum Subset Difference

All use similar logic.

---

# ✅ Final Output

Input:
```
[1,1,1,1,1], target = 3
```

Output:
```
5
```

---

