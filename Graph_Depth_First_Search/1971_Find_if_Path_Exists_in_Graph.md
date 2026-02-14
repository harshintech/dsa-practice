# LeetCode 1971 - Find if Path Exists in Graph (DFS)

---


🔗 **Repository Link:**  
## [Interview-Preparation GitHub Repo Contribute Now 🕊️.](https://github.com/harshintech/Interview-Preparation)


## 📌 Problem

You are given:

- `n` → number of nodes  
- `edges[][]` → undirected edges  
- `source`  
- `destination`  

Return:

```
true  → if path exists
false → otherwise
```

---

## 🧠 Core Idea

This is a basic **Graph Traversal Problem**.

We:

1️⃣ Build an **Adjacency List**  
2️⃣ Use **DFS** (Depth First Search)  
3️⃣ Check if destination is reachable  

---

# 🏗 Step 1: Build Adjacency List

For `n = 5`

We create:

```java
adjList = [
   [],  // 0
   [],  // 1
   [],  // 2
   [],  // 3
   []   // 4
]
```

For edge `[1,3]`:

```
adjList.get(1).add(3);
adjList.get(3).add(1);
```

Because graph is **undirected**.

---

# 💻 Java Code

```java
class Solution {
    public boolean validPath(int n, int[][] edges,
                             int source, int destination) {

        // Step 1: Create adjacency list
        ArrayList<ArrayList<Integer>> adjList =
            new ArrayList<>();

        for(int i = 0; i < n; i++){
            adjList.add(new ArrayList<>());
        }

        // Step 2: Fill edges
        for(int i = 0; i < edges.length; i++){
            int u = edges[i][0];
            int v = edges[i][1];

            adjList.get(u).add(v);
            adjList.get(v).add(u);
        }

        // Step 3: DFS
        boolean[] visited = new boolean[n];

        return dfs(adjList, source,
                   destination, visited);
    }

    public boolean dfs(
        ArrayList<ArrayList<Integer>> adjList,
        int curNode,
        int destination,
        boolean[] visited){

        visited[curNode] = true;

        if(curNode == destination){
            return true;
        }

        for(int neighbour : adjList.get(curNode)){
            if(!visited[neighbour]){
                if(dfs(adjList, neighbour,
                       destination, visited)){
                    return true;
                }
            }
        }

        return false;
    }
}
```

---

# 🎨 Visual Example

Input:

```
n = 3
edges = [[0,1],[1,2]]
source = 0
destination = 2
```

Graph:

```
0 —— 1 —— 2
```

DFS path:

```
0 → 1 → 2
```

Return:
```
true
```

---

# ⏱ Time Complexity

Building graph:
```
O(n + e)
```

DFS traversal:
```
O(n + e)
```

Total:
```
O(n + e)
```

Where:
- `n` = nodes
- `e` = edges

---

# 📦 Space Complexity

```
O(n + e)
```

For adjacency list + visited array.

---

# 🔥 Pattern Used

Graph Traversal  
DFS  
Visited Array  

---

# 🧠 Why Visited Array Is Important?

Without it:

```
Infinite loop in cyclic graphs.
```

Example:
```
0 — 1
 \  /
  2
```

---

# 🏆 Alternative Approaches

You can also solve using:

- BFS (Queue)
- Union-Find (Disjoint Set)

All valid.

---

# ✅ Final Insight

This is a basic:

```
Connectivity Problem
```

If you understand this,
you understand:

- Graph traversal
- DFS recursion
- Adjacency list construction

---

