# 🧠 Path Sum III (Beginner Friendly Explanation)

---

## 📌 Problem

Given the root of a binary tree and an integer `targetSum`,  
return the number of paths where the sum of the values along the path equals `targetSum`.

Important:

- Path does NOT need to start at root.
- Path must go downward (parent → child).

---

## 🧩 Example

Tree:

```
        10
       /  \
      5   -3
     / \     \
    3   2     11
   / \   \
  3  -2   1
```

Target:
```
8
```

Output:
```
3
```

Valid paths:

```
5 → 3
5 → 2 → 1
-3 → 11
```

---

# 🚀 Simple Idea (Prefix Sum)

## 🔑 Core Thought

At every node:

```
currentSum = sum from root to this node
```

If:

```
currentSum - targetSum
```

already exists before,
that means there is a previous path that makes the remaining sum equal to target.

So we:

1. Keep a HashMap of prefix sums.
2. Traverse using DFS.
3. At each node:
   - Add value to running sum.
   - Check if `(currentSum - targetSum)` exists.
4. Increase answer.
5. Backtrack (important).

---

# 💻 Beginner Friendly Code

```java
class Solution {

    int total = 0;

    public void dfs(TreeNode root, int targetSum, long currentSum,
                    Map<Long, Integer> prefixMap) {

        if (root == null) return;

        // Step 1: Update running sum
        currentSum += root.val;

        // Step 2: Check if valid path exists
        if (prefixMap.containsKey(currentSum - targetSum)) {
            total += prefixMap.get(currentSum - targetSum);
        }

        // Step 3: Add current sum to map
        prefixMap.put(currentSum,
                      prefixMap.getOrDefault(currentSum, 0) + 1);

        // Step 4: Go left and right
        dfs(root.left, targetSum, currentSum, prefixMap);
        dfs(root.right, targetSum, currentSum, prefixMap);

        // Step 5: Backtrack (remove current sum)
        prefixMap.put(currentSum, prefixMap.get(currentSum) - 1);
    }

    public int pathSum(TreeNode root, int targetSum) {

        Map<Long, Integer> prefixMap = new HashMap<>();

        // Important: Base case
        prefixMap.put(0L, 1);

        dfs(root, targetSum, 0, prefixMap);

        return total;
    }
}
```

---

# 🎨 Step-by-Step Simple Example

Suppose:

```
target = 8
```

At node 5:

```
currentSum = 15
```

We check:

```
15 - 8 = 7
```

If 7 existed before,
then from that point to current node sum = 8.

That means we found a valid path.

---

# 🧠 Why Backtracking is Important

This line:

```
prefixMap.put(currentSum, prefixMap.get(currentSum) - 1);
```

removes the current path count before returning.

Otherwise:

- Sibling paths would get wrong counts.
- You would count invalid paths.

---

# ⏱ Time Complexity

O(n)

- Each node visited once.

---

# 📦 Space Complexity

O(n)

- HashMap stores prefix sums.
- Recursion stack also O(n) worst case.

---

# 🔥 Pattern Used

Binary Tree  
DFS  
Prefix Sum  
HashMap  
Backtracking  

---

# 🏆 Interview Tip

If interviewer asks:

Why use long instead of int?

Because sum can overflow if values are large.

---

# ✅ Final Output

Input:
```
targetSum = 8
```

Output:
```
3
```

---

# 🎯 Summary (Very Simple)

At every node:

```
currentSum += node.val
check if (currentSum - target) exists
store currentSum
go left
go right
remove currentSum
```

That’s it.

