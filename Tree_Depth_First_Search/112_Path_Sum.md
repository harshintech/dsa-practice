# 🧠 Path Sum (Root to Leaf)

---

## 📌 Problem

Given the root of a binary tree and an integer `targetSum`,  
return `true` if the tree has a **root-to-leaf path** such that adding up all the values along the path equals `targetSum`.

A leaf is a node with no children.

---

## 🧩 Example

Input Tree:

```
        5
       / \
      4   8
     /   / \
    11  13   4
   /  \        \
  7    2        1
```

Target:
```
22
```

Output:
```
true
```

Path:
```
5 → 4 → 11 → 2 = 22
```

---

# 🚀 Approach (DFS – Recursion)

## 🔑 Key Idea

- Traverse tree using DFS.
- Maintain a running sum.
- When reaching a leaf:
  - Check if sum equals target.
- If any path returns true → final answer is true.

---

# 💻 Java Code

```java
class Solution {
    
    public boolean dfs(TreeNode root, int targetSum, int sum){

        if(root == null) return false;

        sum += root.val;

        // Check only at leaf node
        if(root.left == null && root.right == null){
            return sum == targetSum;
        }

        boolean left = dfs(root.left, targetSum, sum);
        boolean right = dfs(root.right, targetSum, sum);

        return left || right;
    }

    public boolean hasPathSum(TreeNode root, int targetSum) {

        if(root == null){
            return false;
        }

        return dfs(root, targetSum, 0);
    }
}
```

---

# 🎨 Graphical Explanation

Tree:

```
        5
       / \
      4   8
     /   / \
    11  13   4
   /  \        \
  7    2        1
```

Target:
```
22
```

---

### Path Exploration

Start:
```
sum = 0
```

Visit 5:
```
sum = 5
```

Visit 4:
```
sum = 9
```

Visit 11:
```
sum = 20
```

Visit 7:
```
sum = 27 ❌
```

Backtrack.

Visit 2:
```
sum = 22 ✅
```

Leaf + sum matches target → return true.

---

# ⏱ Time Complexity

O(n)

- Each node visited once.

---

# 📦 Space Complexity

O(h)

- Recursion stack.
- h = height of tree.
- Worst case O(n) (skewed tree).
- Balanced tree O(log n).

---

# 🧠 Why This Works

We explore every root-to-leaf path.

At each leaf:

```
Check if sum == target
```

If any path satisfies condition → return true immediately.

---

# 🔥 Pattern Used

Binary Tree  
DFS  
Recursion  
Root-to-Leaf Path  

---

# ⚡ Alternative (Cleaner Version)

Instead of passing sum forward:

```java
public boolean hasPathSum(TreeNode root, int targetSum) {

    if(root == null) return false;

    if(root.left == null && root.right == null){
        return targetSum == root.val;
    }

    return hasPathSum(root.left, targetSum - root.val) ||
           hasPathSum(root.right, targetSum - root.val);
}
```

This avoids extra `sum` variable.

---

# ✅ Final Output

Input:
```
targetSum = 22
```

Output:
```
true
```

---

# 🏆 Interview Insight

Always check condition at **leaf node only**.

Checking at non-leaf node would give incorrect results.

