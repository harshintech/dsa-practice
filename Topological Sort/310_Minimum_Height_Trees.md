# 🌳 Minimum Height Trees (Leetcode 310)

---

## 📌 Problem

You are given:

```
n → number of nodes
edges → undirected tree
```

You must return:

```
All possible root nodes
which produce Minimum Height Tree (MHT)
```

---

## 🧠 Important Observation

A tree's **minimum height** occurs when root is placed at:

```
CENTER of tree
```

NOT at leaf nodes.

---

## 🌲 Example

```
      1
     / \
    0   2
         \
          3
```

Heights:

```
Root = 0 → height = 3 ❌
Root = 3 → height = 3 ❌
Root = 1 → height = 2 ✅
Root = 2 → height = 2 ✅
```

Answer:

```
[1,2]
```

---

# 🔥 Core Idea (VERY IMPORTANT)

Instead of finding height from every node ❌

We do:

```
Remove leaves layer by layer
```

Just like:

```
Peeling an onion 🧅
```

Remaining nodes = Tree Center

---

# 🎯 Algorithm Idea

```
Leaf nodes → degree = 1
```

Steps:

1. Build graph
2. Find all leaves
3. Remove leaves
4. Update degrees
5. Repeat until ≤ 2 nodes remain

Remaining nodes = MHT roots

---

# 💻 Code 
```java
class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {

        // Edge case: single node
        if (n == 1) {
            return Arrays.asList(0);
        }

        List<List<Integer>> graph = new ArrayList<>();

        for(int i = 0;i<n;i++){
            graph.add(new ArrayList<>());
        }

         // Degree (indegree in this context)
        int[] degree = new int[n];

        // Build graph
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            graph.get(u).add(v);
            graph.get(v).add(u);
            degree[u]++;
            degree[v]++;
        }

        Queue<Integer> queue = new LinkedList<>();

        for(int i = 0;i<n;i++){
            if(degree[i] == 1){
                queue.offer(i);
            }
        }

        int nodes = n;

        while(nodes > 2){   
            int size = queue.size();
            nodes = nodes - size;

            for(int i = 0;i<size;i++){
                int curr = queue.poll();

                for(int neighbour : graph.get(curr)){
                    degree[neighbour]--;

                    if(degree[neighbour] == 1){
                       queue.offer(neighbour);
                    }
                }
            }
        }

         // Remaining nodes are roots of MHTs
        List<Integer> ans = new ArrayList<>();
        while (!queue.isEmpty()) {
            ans.add(queue.poll());
        }

        return ans;
        
    }
}
```

---

# 🌳 Graphical Visualization

---

## Initial Tree

```
      1
     / \
    0   2
         \
          3
```

Degrees:

```
0 → 1
1 → 2
2 → 2
3 → 1
```

Leaves:

```
[0,3]
```

---

## 🧅 Round 1 — Remove Leaves

Remove:

```
0 , 3
```

Remaining:

```
1 --- 2
```

Now:

```
nodes = 2
```

STOP ✅

---

## ✅ Result

```
[1,2]
```

These are tree centers.

---

# 🧩 Why Stop at ≤ 2 Nodes?

Tree properties:

| Structure | Centers |
|-----------|---------|
| Odd length | 1 center |
| Even length | 2 centers |

So maximum answer size = **2**

---

# ⏱ Complexity

### Time
```
O(V + E)
```

Each node removed once.

---

### Space
```
O(V + E)
```

Graph + Queue.

---

# 🔥 Pattern Recognition

If problem says:

✅ Tree  
✅ Minimum Height  
✅ Best Root  
✅ Center Node  

👉 Think immediately:

```
Topological Trim / Leaf Removal
```

---

# 🚀 Interview Insight

This is actually:

```
Reverse Topological Sort on Undirected Tree
```

Very famous Google / Amazon question.

---

# 🏆 Key Intuition (Golden Line)

```
Minimum Height Tree roots
= Centers of Tree
= Nodes left after removing all leaves repeatedly
```

---

