# 🎒 0/1 Knapsack (1D DP Optimization)

---

## 📌 Problem

You are given:

- `val[]` → values of items  
- `wt[]` → weights of items  
- `W` → maximum capacity  

Each item can be taken:

```
At most once (0/1 Knapsack)
```

Return the **maximum total value**.

---

## 🧩 Example

```
val = [1, 2, 3]
wt  = [4, 5, 1]
W   = 4
```

---

## 🎯 Explanation

We must choose items such that:

```
Total weight ≤ 4
```

Possible choices:

| Items Chosen | Weight | Value |
|--------------|--------|-------|
| Item 1 | 4 | 1 |
| Item 3 | 1 | 3 |
| Item 1 + 3 | 5 ❌ | - |

Best valid choice:

```
Item 3 → Value = 3
```

Output:
```
3
```

---

# 🚀 Approach (1D Dynamic Programming)

---

## 🔑 Core Idea

We create:

```
dp[j]
```

Meaning:

```
Maximum value achievable with capacity j
```

---

### For each item:

We decide:

```
Take it OR Leave it
```

Transition:

```
dp[j] = max(
    dp[j],
    dp[j - weight] + value
)
```

---

# 💻 JavaScript Code

```javascript
function knapsack(W, val, wt) {

    // Initialize dp array
    let dp = new Array(W + 1).fill(0);

    // Iterate over items
    for (let i = 1; i <= wt.length; i++) {

        // Go backwards (important!)
        for (let j = W; j >= wt[i - 1]; j--) {

            dp[j] = Math.max(
                dp[j],
                dp[j - wt[i - 1]] + val[i - 1]
            );
        }
    }

    return dp[W];
}

// Driver Code
let val = [1, 2, 3];
let wt = [4, 5, 1];
let W = 4;

console.log(knapsack(W, val, wt));
```

---

# 🧠 Why Iterate Backwards?

```
for (j = W → weight)
```

Because:

This is **0/1 Knapsack**

Each item must be used **only once**.

If we go forward:

```
j = weight → W
```

We might reuse the same item multiple times (which becomes Unbounded Knapsack).

---

# 🧠 Dry Run

Initial:
```
dp = [0,0,0,0,0]
```

---

### Item 1 (weight=4, value=1)

Update:

```
dp[4] = 1
```

---

### Item 2 (weight=5)

Ignored (weight > capacity)

---

### Item 3 (weight=1, value=3)

Update:

```
dp[1] = 3
dp[2] = 3
dp[3] = 3
dp[4] = max(1, dp[3]+3) = 3
```

Final:
```
dp = [0,3,3,3,3]
```

Answer:
```
3
```

---

# ⏱ Time Complexity

```
O(n × W)
```

Where:

- n = number of items
- W = capacity

---

# 📦 Space Complexity

```
O(W)
```

1D optimized DP.

---

# 🔥 Pattern Used

0/1 Knapsack  
Dynamic Programming  
Space Optimization  

---

# 🏆 Compare With Variants

| Type | Loop Direction | Reuse Allowed? |
|------|---------------|----------------|
| 0/1 Knapsack | Backward | ❌ No |
| Unbounded Knapsack | Forward | ✅ Yes |

---

# 🧠 Interview Insight

Whenever problem says:

```
Each item can be used once
```

Think:

```
0/1 Knapsack
Backward iteration
```

---

# ✅ Final Output

```
3
```

---

