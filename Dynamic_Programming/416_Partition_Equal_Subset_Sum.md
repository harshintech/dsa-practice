# 🎯 Partition Equal Subset Sum (0/1 Knapsack)

---

## 📌 Problem

Given an array `nums`, return:

```
true  → if it can be partitioned into two subsets with equal sum
false → otherwise
```

---

## 🧩 Example

Input:
```
nums = [1,2,3,2,2,1,1]
```

Total sum:
```
12
```

Target:
```
12 / 2 = 6
```

Possible partition:

```
Set A: [1,2,3] → 6
Set B: [2,2,1,1] → 6
```

Output:
```
true
```

---

# 🚀 Approach (0/1 Knapsack – Subset Sum)

---

## 🔑 Core Idea

If total sum is odd → impossible.

If total sum is even:

We just need to check:

```
Can we form subset with sum = total/2 ?
```

This is classic:

```
Subset Sum Problem
```

---

# 💻 Java Code

```java
class Solution {
    public boolean canPartition(int[] nums) {

        int sum = 0;

        for(int n : nums){
            sum += n;
        }

        // If sum is odd → cannot divide
        if(sum % 2 == 1)
            return false;

        int target = sum / 2;

        boolean[] dp = new boolean[target + 1];
        dp[0] = true;

        for(int num : nums){

            // Go backwards (0/1 constraint)
            for(int j = target; j >= num; j--){

                if(dp[j - num]){
                    dp[j] = true;
                }
            }
        }

        return dp[target];
    }
}
```

---

# 🧠 Why Iterate Backwards?

```
for (j = target → num)
```

Because:

We are solving **0/1 Knapsack**

Each number can be used **only once**.

If we go forward:

```
j = num → target
```

We may reuse same number multiple times.

Backward ensures:

```
Previous state is used.
```

---

# 🧠 DP Meaning

```
dp[j] = true
```

Means:

```
Sum j is possible using some elements.
```

---

# 🧠 Dry Run Example

Input:
```
[1,2,3,2,2,1,1]
Target = 6
```

Start:
```
dp[0] = true
```

Process 1:
```
dp[1] = true
```

Process 2:
```
dp[2] = true
dp[3] = true
```

Process 3:
```
dp[6] = true
```

Once:
```
dp[target] = true
```

We can stop thinking.

---

# ⏱ Time Complexity

```
O(n × target)
```

Where:

```
target = sum/2
```

---

# 📦 Space Complexity

```
O(target)
```

---

# 🔥 Pattern Used

0/1 Knapsack  
Subset Sum  
1D Dynamic Programming  

---

# 🏆 Why This Is Important

This is a foundational DP problem.

Many problems reduce to:

```
Subset Sum
```

Examples:

- Target Sum
- Count Subsets
- Minimum Subset Difference

---

# ⚠ Important Insight

If total sum is odd:

```
Immediate return false
```

No need for DP.

---

# 🧠 Interview Insight

Whenever problem says:

```
Divide array into two equal parts
```

Think:

```
Total Sum / 2
Subset Sum
```

---

# ✅ Final Output

Input:
```
[1,2,3,2,2,1,1]
```

Output:
```
true
```

---


