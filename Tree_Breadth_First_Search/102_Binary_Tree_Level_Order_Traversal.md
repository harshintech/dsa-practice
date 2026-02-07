# 🧠 Binary Tree Level Order Traversal

---

## 📌 Problem

Given the root of a binary tree,  
return the level order traversal of its nodes' values.

(Level order means: left to right, level by level.)

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

Output:
```
[[3], [9,20], [15,7]]
```

---

# 🚀 Approach (BFS – Breadth First Search)

## 🔑 Key Idea

- Use a **Queue**.
- Traverse the tree level by level.
- For each level:
  - Process all nodes currently in queue.
  - Add their children to queue.
- Store each level in a separate list.

---

# 💻 Java Code

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {

        List<List<Integer>> ans = new ArrayList<>();

        if(root == null){
            return ans;
        }

        Queue<TreeNode> queue = new LinkedList<>();
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

            ans.add(list);
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

Add children:
```
[9, 20]
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

Add children:
```
[15, 7]
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

No more children.

---

Final Output:

```
[[3], [9,20], [15,7]]
```

---

# ⏱ Time Complexity

O(n)

- Each node visited once.

---

# 📦 Space Complexity

O(n)

- Queue stores nodes of one level.
- In worst case (complete tree), last level has n/2 nodes.

---

# 🧠 Why This Works

BFS naturally processes nodes level by level.

Using:

```
int size = queue.size();
```

Ensures we only process nodes of current level.

---

# 🔥 Pattern Used

Binary Tree  
Breadth First Search (BFS)  
Queue  
Level Order Traversal  

---

# ⚡ Interview Insight

If interviewer asks:

Why not DFS?

DFS can also do level order, but BFS is more natural and simpler for this problem.

---

# ✅ Final Output

Input:
```
[3,9,20,null,null,15,7]
```

Output:
```
[[3], [9,20], [15,7]]
```

