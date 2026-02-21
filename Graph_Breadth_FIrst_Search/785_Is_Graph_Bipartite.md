# 🎨 Bipartite Graph (DFS | BFS | Union Find)

---

# 📌 Problem

Given a graph:

```
graph[i] → neighbours of node i
```

Determine:

```
Is graph Bipartite ?
```

---

## 🎯 What is Bipartite Graph?

A graph is bipartite if:

```
Nodes can be divided into TWO groups
such that NO adjacent nodes share same group.
```

Equivalent Meaning:

```
Graph can be colored using ONLY 2 colors.
```

Example ✅

```
0 ---- 1
|      |
3 ---- 2
```

Coloring:

```
Set A → {0,2}
Set B → {1,3}
```

---

## ❌ Non Bipartite Example

Odd Cycle:

```
0 --- 1
 \   /
   2
```

Impossible to 2-color.

---

# 🧠 Core Idea

```
Adjacent nodes must have opposite colors.
```

We use:

```
color[i] = 0 or 1
-1 → uncolored
```

---

---

# ✅ APPROACH 1 — DFS Coloring

---

## 💡 Idea

1. Start DFS
2. Assign color
3. Neighbor gets opposite color
4. Conflict → Not Bipartite

---

## ✅ Code

```java
class Solution {

    public boolean dfs(int curr, int col, int[] color, int[][] graph) {

        // assign color to current node
        color[curr] = col;

        for(int neigh : graph[curr]) {

            // if neighbour not colored
            if(color[neigh] == -1) {

                // color with opposite color
                if(!dfs(neigh, 1 - col, color, graph))
                    return false;
            }
            // conflict: same color
            else if(color[neigh] == col) {
                return false;
            }
        }

        return true;
    }

    public boolean isBipartite(int[][] graph) {

        int n = graph.length;
        int[] color = new int[n];

        // initially uncolored
        for(int i = 0; i < n; i++)
            color[i] = -1;

        // handle disconnected components
        for(int i = 0; i < n; i++) {

            if(color[i] == -1) {
                if(!dfs(i, 0, color, graph))
                    return false;
            }
        }

        return true;
    }
}
```

---

## ⏱ Complexity

```
Time  : O(V + E)
Space : O(V) recursion stack
```

---

---

# ✅ APPROACH 2 — BFS Coloring

---

## 💡 Idea

Same logic as DFS but using Queue.

```
Level by level coloring
```

---

## ✅ Code 

```java
class Solution {
    public boolean isBipartite(int[][] graph) {
        int n = graph.length;
        int[] color = new int[n];

        Arrays.fill(color,-1); //not colored

        for(int i = 0;i<n;i++){

            //handle disconnected graph
            if(color[i] == - 1){
                Queue<Integer> q = new LinkedList<>();
                q.offer(i);
                color[i] = 0;

                while(!q.isEmpty()){

                    int curr = q.poll();

                    for(int neighbour : graph[curr]){

                        //not colored
                        if(color[neighbour] == -1){
                            color[neighbour]  = 1 - color[curr]; //--> 0 or 1
                            q.offer(neighbour);
                        }else if(color[neighbour] ==  color[curr]) {
                            return false;
                        }
                    }
                }
            }
        }

        return true;
    }
}
```

---

## ⏱ Complexity

```
Time  : O(V + E)
Space : O(V)
```

---

---

# ✅ APPROACH 3 — Union Find (DSU)

---

## 💡 Advanced Idea

Key Observation:

```
All neighbours of a node
must belong to SAME opposite group.
```

So:

```
Union all neighbours together.
```

If node and neighbour end up same parent → conflict.

---

## ✅ Code 

```java
class Solution {

    int[] parent;

    int find(int x){
        if(parent[x] == x)
            return x;

        return parent[x] = find(parent[x]);
    }

    void union(int a, int b){
        int pa = find(a);
        int pb = find(b);

        if(pa != pb)
            parent[pb] = pa;   // ✅ changed direction
    }

    public boolean isBipartite(int[][] graph) {

        int n = graph.length;
        parent = new int[n];

        for(int i = 0; i < n; i++)
            parent[i] = i;

        for(int u = 0; u < n; u++) {

            if(graph[u].length == 0)
                continue;

            for(int v : graph[u]) {

                // conflict check
                if(find(u) == find(v))
                    return false;

                // union neighbours
                union(graph[u][0], v);
            }
        }

        return true;
    }
}
```

---

## ⏱ Complexity

```
Time  : O(E α(N))
Space : O(N)
```

(Almost constant)

---

---

# 🧩 Comparison

| Method | Difficulty | Interview Use |
|------|------|------|
| DFS | ⭐ Easy | Very Common |
| BFS | ⭐ Easy | Very Common |
| Union Find | ⭐⭐⭐ Advanced | FAANG Level |

---

---

# 🔥 Pattern Recognition

If problem mentions:

```
2 groups
no conflict
enemy/friend
odd cycle
two teams
```

👉 Think instantly:

```
BIPARTITE GRAPH
```

---

# 🏆 Golden Interview Insight

```
Graph is Bipartite
⇢ if and only if
Graph has NO odd-length cycle.
```

---



