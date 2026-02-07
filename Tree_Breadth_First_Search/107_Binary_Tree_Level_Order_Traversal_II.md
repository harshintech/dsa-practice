# 🧠 Binary Tree Level Order Traversal II (Bottom-Up)

---

## 📌 Problem

Given the root of a binary tree,  
return the **bottom-up level order traversal** of its nodes' values.

That means:

- Traverse level by level.
- But return levels from bottom to top.

---

## 🧩 Example

Input Tree:

```
        3
       / \
      9  20
         /  \
        15   7
```

Normal Level Order:
```
[[3], [9,20], [15,7]]
```

Bottom-Up Output:
```
[[15,7], [9,20], [3]]
```

---

# 🚀 Approach (BFS + Insert at Front)

## 🔑 Key Idea

- Use **BFS (Queue)** to traverse level by level.
- For each level:
  - Collect nodes.
  - Insert that level at index `0` in result list.

This automatically builds bottom-up order.

---

# 💻 Java Code

```java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {

        List<List<Integer>> ans = new ArrayList<>();

        if(root == null){
            return ans;
        }

        Queue<TreeNode> queue = new ArrayDeque<>();
        queue.add(root);

        while(!queue.isEmpty()){

            int size = queue.size();
            List<Integer> list = new ArrayList<>();

            for(int i = 0; i < size; i++){

                TreeNode curr = queue.remove();

                if(curr.left != null) queue.add(curr.left);
                if(curr.right != null) queue.add(curr.right);

                list.add(curr.val);
            }

            ans.add(0, list);   // insert at beginning
        }

        return ans;
    }
}
```

---

# 🎨 Graphical Explanation

Tree:

```
        3
       / \
      9  20
         /  \
        15   7
```

---

### Step 1

Queue:
```
[3]
```

Process level:
```
[3]
```

Insert at front:
```
[[3]]
```

---

### Step 2

Queue:
```
[9, 20]
```

Process level:
```
[9, 20]
```

Insert at front:
```
[[9,20], [3]]
```

---

### Step 3

Queue:
```
[15, 7]
```

Process level:
```
[15, 7]
```

Insert at front:
```
[[15,7], [9,20], [3]]
```

---

# 🎉 Final Output

```
[[15,7], [9,20], [3]]
```

---

# ⏱ Time Complexity

O(n)

- Each node visited once.

---

# 📦 Space Complexity

O(n)

- Queue stores nodes.
- Result list stores all nodes.

---

# 🧠 Important Note

Using:

```
ans.add(0, list);
```

inserts at the beginning.

But this operation takes O(n) time internally.

---

# ⚡ More Optimal Alternative

Instead of inserting at index 0, you can:

1. Perform normal level order.
2. Reverse the result at the end.

Example idea:

```
Collections.reverse(ans);
```

This avoids repeated shifting.

---

# 🔥 Pattern Used

Binary Tree  
BFS  
Queue  
Level Order Traversal  

---

# 🏆 Interview Insight

Difference from normal level order:

Normal:
```
ans.add(list);
```

Bottom-Up:
```
ans.add(0, list);
```

Or reverse at end.

---

# ✅ Final Output

Input:
```
[3,9,20,null,null,15,7]
```

Output:
```
[[15,7], [9,20], [3]]
```

![itachiuchiha.png](https://assets.leetcode.com/users/images/4bbe2c9f-acd3-4161-9b72-ad6cf53c2d18_1770438506.0334132.png)
