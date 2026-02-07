# 🧠 Diameter of Binary Tree

---

## 📌 Problem

Given the root of a binary tree,  
return the **length of the diameter** of the tree.

The diameter is:

> The length of the longest path between any two nodes in the tree.

Important:
- The path may or may not pass through the root.
- Length is counted in **number of edges**.

---

## 🧩 Example

Tree:

```
        1
       / \
      2   3
     / \
    4   5
```

Longest path:

```
4 → 2 → 1 → 3
```

Diameter:
```
3
```

(3 edges)

---

# 🚀 Approach (DFS + Height Calculation)

## 🔑 Key Idea

At every node:

- Compute left subtree height → `l`
- Compute right subtree height → `r`
- Possible diameter at this node:

```
l + r
```

Update global maximum.

Return height of current node:

```
max(l, r) + 1
```

---

# 💻 Java Code

```java
class Solution {

    int max = 0;

    public int findDiam(TreeNode root){

        if(root == null){
            return 0;
        }

        int l = findDiam(root.left);
        int r = findDiam(root.right);

        // Update diameter
        max = Math.max(max, l + r);

        // Return height
        return Math.max(l, r) + 1;
    }

    public int diameterOfBinaryTree(TreeNode root) {

        findDiam(root);

        return max;
    }
}
```

---

# 🎨 Step-by-Step Explanation

Tree:

```
        1
       / \
      2   3
     / \
    4   5
```

---

### Node 4

```
l = 0
r = 0
height = 1
```

---

### Node 5

```
l = 0
r = 0
height = 1
```

---

### Node 2

```
l = 1
r = 1
diameter candidate = 2
height = 2
```

---

### Node 3

```
height = 1
```

---

### Node 1

```
l = 2
r = 1
diameter candidate = 3
```

Final max:
```
3
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

Worst case:
- Skewed tree → O(n)

Balanced tree:
- O(log n)

---

# 🧠 Why This Works

The longest path through any node equals:

```
height(left) + height(right)
```

So while computing height,
we simultaneously compute diameter.

One DFS does both.

---

# 🔥 Pattern Used

Binary Tree  
DFS  
Height Calculation  
Global Variable Tracking  

---

# ⚠ Important Concept

Height = number of nodes from current node to deepest leaf.

Diameter = number of edges.

That’s why:

```
max = l + r
```

(not +1)

---

# 🏆 Interview Insight

If interviewer asks:

Why not compute height separately?

Because that would be O(n²).

This solution does both in one DFS → O(n).

---

# ✅ Final Output

Input:
```
[1,2,3,4,5]
```

Output:
```
3
```

