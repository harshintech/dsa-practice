# 🌍 Number of Provinces (DFS on Graph)

---

## 📌 Problem

You are given an adjacency matrix:

```
isConnected[i][j] = 1 → city i and city j are directly connected
isConnected[i][j] = 0 → not connected
```

A province is a group of directly or indirectly connected cities.

Return the **number of provinces**.

---

## 🧩 Example

Input:
```
isConnected = [
 [1,1,0],
 [1,1,0],
 [0,0,1]
]
```

Graph Representation:

```
0 —— 1     2
```

Output:
```
2
```

Because:

- {0,1} is one province
- {2} is another province

---

# 🚀 Approach (DFS – Connected Components)

---

## 🔑 Core Idea

This is a **Connected Components Problem**.

Steps:

1️⃣ Treat each city as a node  
2️⃣ Use DFS to visit all connected cities  
3️⃣ Every time we start DFS from an unvisited node → new province  

---

# 💻 Optimized DFS (Without Building Extra Graph)

```java
class Solution {

    public int findCircleNum(int[][] isConnected) {

        int n = isConnected.length;
        boolean[] visited = new boolean[n];

        int count = 0;

        for(int i = 0; i < n; i++){
            if(!visited[i]){
                count++;
                dfs(i, isConnected, visited);
            }
        }

        return count;
    }

    public void dfs(int city,
                    int[][] graph,
                    boolean[] visited){

        visited[city] = true;

        for(int j = 0; j < graph.length; j++){
            if(graph[city][j] == 1 && !visited[j]){
                dfs(j, graph, visited);
            }
        }
    }
}
```

# 💻 Union-Find (Disjoint Set)

```java
class DSU {
    int[] parent, size;

    DSU(int n) {
        parent = new int[n];
        size = new int[n];

        for (int i = 0; i < n; i++) {
            parent[i] = i;
            size[i] = 1;
        }
    }

    int findParent(int x) {
        if (parent[x] == x)
            return x;
        return parent[x] = findParent(parent[x]);
    }

    public void unionBySize(int u, int v) {
        int pu = findParent(u);
        int pv = findParent(v);

        if (pu == pv)
            return;

        if (size[pu] < size[pv]) {
            parent[pu] = pv;
            size[pv] += size[pv];
        } else {
            parent[pv] = pu;
            size[pu] += size[pv];
        }
    }
}

class Solution {

    public int findCircleNum(int[][] isConnected) {
        int n = isConnected.length;
        DSU dsu = new DSU(n);

        for(int i = 0;i<n;i++){
            for(int j = i + 1;j<n;j++){
                if(isConnected[i][j] == 1){
                    dsu.unionBySize(i,j);
                }
            }
        }

        int provinces = 0;
        for (int i = 0; i < n; i++) {
            if (dsu.findParent(i) == i) provinces++;
        }

        return provinces;
        
    }
}
```

---

# 🧠 Why We Don't Need Adjacency List?

Because:

We already have adjacency matrix.

Building extra graph:

```
Unnecessary O(n²) work
```

We can directly traverse matrix.

Cleaner + optimal.

---

# 🎨 Visual Explanation

Matrix:

```
1 1 0
1 1 0
0 0 1
```

DFS flow:

Start at 0:
```
0 → 1
```
Mark both visited.

Next unvisited: 2
```
2 alone
```

Total provinces:
```
2
```

---

# ⏱ Time Complexity

```
O(n²)
```

Because:

- Matrix traversal inside DFS.

---

# 📦 Space Complexity

```
O(n)
```

For visited array.

---

# 🔥 Pattern Used

Graph Traversal  
DFS  
Connected Components  

---

# 🏆 Alternative Solutions

You can also solve using:

- BFS
- Union-Find (Disjoint Set)

Union-Find is very popular for this problem.

---

# 🧠 Interview Insight

This problem tests:

- Understanding of graph components
- DFS basics
- Matrix graph traversal

Very common beginner graph question.

---

# ✅ Final Answer

Input:
```
[[1,1,0],
 [1,1,0],
 [0,0,1]]
```

Output:
```
2
```




