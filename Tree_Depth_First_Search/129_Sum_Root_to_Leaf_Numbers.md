# 🧠 Sum Root to Leaf Numbers

---

## 📌 Problem

You are given the root of a binary tree containing digits (0–9).

Each root-to-leaf path represents a number.

Return the total sum of all root-to-leaf numbers.

---

## 🧩 Example

Tree:

```
        1
       / \
      2   3
```

Paths:

```
1 → 2  = 12
1 → 3  = 13
```

Output:
```
12 + 13 = 25
```

---

# 🚀 Approach (DFS + Carry Forward Number)

## 🔑 Key Idea

At each node:

```
currentNumber = previousNumber * 10 + node.val
```

This builds the number digit by digit.

When we reach a **leaf node**,  
we return the full number.

Then we sum left and right results.

---

# 💻 Java Code

```java
class Solution {

    public int findSum(TreeNode root, int sum){

        if(root == null){
            return 0;
        }

        sum = sum * 10 + root.val;

        // If leaf node → return formed number
        if(root.left == null && root.right == null){
            return sum;
        }

        int leftSum = findSum(root.left, sum);
        int rightSum = findSum(root.right, sum);

        return leftSum + rightSum;
    }

    public int sumNumbers(TreeNode root) {
        return findSum(root, 0);
    }
}
```

---

# 🎨 Step-by-Step Explanation

Example:

```
        4
       / \
      9   0
     / \
    5   1
```

---

### Path 1

```
4 → 9 → 5
```

Calculation:

```
0 * 10 + 4 = 4
4 * 10 + 9 = 49
49 * 10 + 5 = 495
```

---

### Path 2

```
4 → 9 → 1
```

Calculation:

```
49 * 10 + 1 = 491
```

---

### Path 3

```
4 → 0
```

Calculation:

```
4 * 10 + 0 = 40
```

---

### Final Sum

```
495 + 491 + 40 = 1026
```

---

# ⏱ Time Complexity

O(n)

- Each node visited once.

---

# 📦 Space Complexity

O(h)

- Recursion stack.
- h = height of tree.
- Worst case O(n).

---

# 🧠 Important Mistake to Avoid

Wrong:

```
if(root == null) return sum;
```

Correct:

```
if(root == null) return 0;
```

Why?

Because null node does NOT represent a valid path.

Only leaf node should return sum.

---

# 🔥 Pattern Used

Binary Tree  
DFS  
Carry Forward Value  
Root-to-Leaf Path  

---

# 🏆 Interview Insight

This is a classic:

“Carry forward calculation in recursion”

Similar pattern used in:

- Path Sum
- Binary Number from Root to Leaf
- Maximum Path Value

---

# ✅ Final Output

Input:
```
[4,9,0,5,1]
```

Output:
```
1026
```

![itachiuchiha.png](https://assets.leetcode.com/users/images/956729b2-5c61-438c-80a9-6cea64230cd3_1770467827.973659.png)
