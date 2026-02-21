# 🔗 Redundant Connection (Union Find / DSU)

---

## 📌 Problem

You are given a graph that was originally a **tree**.

A tree has:

```
N nodes
N-1 edges
NO cycle
```

But one extra edge was added.

👉 That extra edge creates a **cycle**.

---

## 🎯 Goal

Return the edge that creates the cycle.

```
Redundant Edge
```

---

## 🧠 Core Idea

A cycle occurs when:

```
Two nodes already belong to SAME connected component
```

So we need a structure that quickly tells:

```
Are these nodes already connected?
```

✅ Solution:

```
Disjoint Set Union (DSU)
aka
Union Find
```

---

# 🔥 Union Find Concept

Each node belongs to a **set**.

Initially:

```
Every node is its own parent.
```

Example:

```
1   2   3   4
```

Parent array:

```
[1,2,3,4]
```

---

# 🧩 Two Main Operations

---

## ✅ 1. Find Parent (findUPar)

Find **ultimate parent** of node.

Also performs:

```
Path Compression
```

which makes future searches faster.

---

## ✅ 2. Union

Connect two components.

If parents already same:

```
Cycle detected 🚨
```

---

# 💻 Code (UNCHANGED ✅)

```java
class Solution {

    int[] parent;

    public int findUPar(int x){
        if(parent[x] == x){
            return x;
        }

        return parent[x] = findUPar(parent[x]);
    }

    //union operation 
    public boolean union(int u,int v){
        int pu = findUPar(u);
        int pv = findUPar(v);

        //already connected -> cycle

        if(pu == pv){
            return false;
        }

        parent[pv] = pu;
        return true;
    }
    
    public int[] findRedundantConnection(int[][] edges) {
        
        int n = edges.length;
        parent = new int[n + 1];

        for(int i = 1;i<=n;i++){
            parent[i] = i;
        }

        for(int[] edge: edges){
            int u = edge[0];
            int v = edge[1];

            if(!union(u,v)){
                return edge;
            }
        }

        return new int[]{};
    }
}
```

---

# 🌳 Step-by-Step Dry Run

Edges:

```
[1,2]
[1,3]
[2,3]
```

---

## Step 1

Union(1,2)

```
1 ← 2
```

No cycle ✅

---

## Step 2

Union(1,3)

```
1 ← 3
```

No cycle ✅

---

## Step 3

Union(2,3)

Find parents:

```
parent(2) → 1
parent(3) → 1
```

Same parent ❌

Cycle detected.

Return:

```
[2,3]
```

---

# 🧠 Visualization

Before redundant edge:

```
    1
   / \
  2   3
```

Adding:

```
2 --- 3
```

creates loop 🔁

---

# ⚡ Path Compression Magic

This line:

```
parent[x] = findUPar(parent[x])
```

Flattens tree:

```
Deep tree → Flat tree
```

Makes operations nearly constant time.

---

# ⏱ Complexity

### Time
```
O(N * α(N))
```

α(N) = inverse Ackermann function  
(almost constant)

---

### Space
```
O(N)
```

Parent array.

---

# 🔥 Pattern Recognition

If problem says:

✅ Detect cycle  
✅ Connected components  
✅ Network connection  
✅ Graph merging  
✅ Extra edge  

👉 Think instantly:

```
Union Find (DSU)
```

---

# 🏆 Interview Golden Line

```
Cycle exists
⇢ when two nodes already share same ultimate parent.
```

---

# 🚀 Advanced Upgrade

Next DSU problems:

✅ Number of Provinces (DSU version)  
✅ Accounts Merge  
✅ Kruskal MST  
✅ Number of Islands II  
✅ Largest Component Size  

---

