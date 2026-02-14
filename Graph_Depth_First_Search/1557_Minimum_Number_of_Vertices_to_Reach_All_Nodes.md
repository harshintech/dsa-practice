# LeetCode 1557 - Minimum Number of Vertices to Reach All Nodes

---


🔗 **Repository Link:**  
## [Interview-Preparation GitHub Repo Contribute Now 🕊️.](https://github.com/harshintech/Interview-Preparation)


## 📌 Problem

You are given:

- `n` → number of nodes (0 to n-1)
- `edges` → directed edges

Return the **smallest set of vertices** from which all nodes in the graph are reachable.

---

## 🧩 Example

Input:
```
n = 6
edges = [[0,1],[0,2],[2,5],[3,4],[4,2]]
```

Graph:

```
0 → 1
↓
2 → 5

3 → 4 → 2
```

Output:
```
[0,3]
```

---

# 🚀 Approach (Indegree Concept)

---

## 🔑 Key Observation

In a **Directed Graph**:

Any node with **indegree = 0**  
must be included in the answer.

Why?

Because:

If a node has indegree > 0,  
it can be reached from some other node.

But if indegree = 0:

👉 No one points to it.  
👉 Only it can start the path.

---

# 💻 Java Code

```java
class Solution {
    public List<Integer> findSmallestSetOfVertices(int n,
                        List<List<Integer>> edges) {

         int[] indegree = new int[n];

         // Step 1: Count indegree
         for(List<Integer> edge : edges){
            indegree[edge.get(1)]++;
         }

         // Step 2: Collect nodes with indegree 0
         List<Integer> list = new ArrayList<>();

         for(int i = 0; i < n; i++){
            if(indegree[i] == 0)
                list.add(i);
         }

         return list;
    }
}
```

---

# 🎯 Why This Works

Suppose node `x` has:

```
indegree = 0
```

That means:

No incoming edges.

So no other node can reach `x`.

Therefore:

We must include `x` in starting set.

---

# 🧠 Dry Run

Input:
```
n = 6
edges = [[0,1],[0,2],[2,5],[3,4],[4,2]]
```

Indegree array:

```
0 → 0
1 → 1
2 → 2
3 → 0
4 → 1
5 → 1
```

Nodes with indegree 0:

```
[0, 3]
```

---

# ⏱ Time Complexity

```
O(n + e)
```

Where:
- `n` = nodes
- `e` = edges

---

# 📦 Space Complexity

```
O(n)
```

For indegree array.

---

# 🔥 Pattern Used

Graph  
Indegree counting  
Directed graph property  

---

# 🏆 Interview Insight

This problem is simpler than it looks.

No DFS needed.  
No BFS needed.  
No Union-Find needed.

Just understand:

```
Nodes with indegree 0 are the answer.
```

---

# ✅ Final Output

Input:
```
n = 6
```

Output:
```
[0,3]
```

---

