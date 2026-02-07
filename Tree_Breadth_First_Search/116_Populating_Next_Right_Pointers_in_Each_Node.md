# LeetCode 116 - Populating Next Right Pointers in Each Node (Perfect Binary Tree)

---

## 📌 Problem

You are given a **perfect binary tree** where:

- Every parent has exactly 2 children
- All leaves are at the same level

Populate each `next` pointer to point to its next right node.  
If there is no next right node, the `next` pointer should be `null`.

---

## 🧩 Example

Input Tree:

```
        1
       / \
      2   3
     / \ / \
    4  5 6  7
```

Output (Next pointers):

```
1 → null
2 → 3 → null
4 → 5 → 6 → 7 → null
```

---

# 🚀 Approach (Constant Space – Level Traversal)

## 🔑 Key Idea

Since the tree is **perfect**, we can:

- Connect:
  ```
  left child → right child
  ```
- And also connect across subtrees:
  ```
  right child → next node's left child
  ```

We use:

```
leftMost → start of each level
cur → iterate across level using next pointers
```

No queue required.

---

# 💻 Java Code

```java
class Solution {
    public Node connect(Node root) {
      
        if(root == null){
            return root;
        }

        Node leftMost = root;
        
        while(leftMost.left != null){

            Node cur = leftMost;
           
            while(cur != null){

                // Connect left → right
                cur.left.next = cur.right;
               
                // Connect right → next subtree's left
                if(cur.next != null){
                    cur.right.next = cur.next.left;
                }

                cur = cur.next;
            }
            
            leftMost = leftMost.left;
        }

        return root;
    }
}
```

---

# 🎨 Graphical Explanation

Tree:

```
        1
       / \
      2   3
     / \ / \
    4  5 6  7
```

---

## Level 1

Connect:
```
2 → 3
```

---

## Level 2

Inside while loop:

For node 2:

```
4 → 5
5 → 6
```

For node 3:

```
6 → 7
```

Final level:

```
4 → 5 → 6 → 7
```

---

# 🧠 Why This Works

Because tree is **perfect**:

- Every node has left & right child.
- `cur.next.left` always exists when `cur.next != null`.

This guarantees safe linking.

---

# ⏱ Time Complexity

O(n)

- Each node visited once.

---

# 📦 Space Complexity

O(1)

- No extra data structures.
- Only pointers used.

---

# 🔥 Pattern Used

Binary Tree  
Level Traversal  
Pointer Manipulation  
Perfect Tree Optimization  

---

# ⚠ Important

This solution ONLY works for:

```
Perfect Binary Tree
```

If tree is not perfect, this approach will fail.

For non-perfect tree, use BFS (queue).

---

# 🏆 Interview Insight

If interviewer asks:

Why no queue?

Because perfect tree property allows us to use already established `next` pointers to traverse level.

---

# ✅ Final Output

Input:
```
[1,2,3,4,5,6,7]
```

Next pointers:

```
1 → null
2 → 3 → null
4 → 5 → 6 → 7 → null
```

