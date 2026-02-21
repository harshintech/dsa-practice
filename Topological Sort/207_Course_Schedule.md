# 🎓 Course Schedule (Topological Sort - Kahn's Algorithm)

---

## 📌 Problem

You are given:

```
numCourses → total courses
prerequisites → dependency list
```

Each pair:

```
[a, b]
```

means:

```
To take course a,
you must first complete course b
```

---

## 🎯 Goal

Return:

```
true  → if all courses can be finished
false → if impossible
```

---

## 🧠 Core Concept

This problem is asking:

```
Does the directed graph contain a cycle?
```

Because:

✅ No Cycle → Courses possible  
❌ Cycle → Infinite dependency  

---

# 🚀 Approach Used

```
Topological Sort (Kahn’s Algorithm)
```

Using:

- Graph (Adjacency List)
- In-degree Array
- Queue (BFS)

---

# 🔗 Graph Meaning

For prerequisite:

```
[u, v]
```

We create edge:

```
v → u
```

Meaning:

```
v must be completed before u
```

---

# 💻 Code

```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        List<List<Integer>> graph = new ArrayList<>();

        for (int i = 0; i < numCourses; i++) {
            graph.add(new ArrayList<>());
        }

        int[] inDegree = new int[numCourses];
        for (int i = 0; i < prerequisites.length; i++) {
            int u = prerequisites[i][0];
            int v = prerequisites[i][1];

            // 2. Directed edge only (usually v -> u means v is a prereq for u)
            graph.get(v).add(u);
            inDegree[u]++;
        }

        //Call your logic (The "Topo Sort" part)
        return solveUsingKahn(numCourses, graph, inDegree);
    }

    private boolean solveUsingKahn(int numCourses,List<List<Integer>> graph,int[] inDegree){
        Queue<Integer> queue = new LinkedList<>();

        for(int i = 0;i<numCourses;i++){
            if(inDegree[i] == 0){
                queue.add(i);
            }
        }

        int count = 0;

        while(!queue.isEmpty()){
            int current = queue.poll();
            count++;

            for(int neighbor : graph.get(current)){
                inDegree[neighbor]--;
                if(inDegree[neighbor] == 0){
                    queue.add(neighbor);
                }
            }
        }

        return count == numCourses;
    }
}
```

---

# 🌳 Algorithm Steps

---

## ✅ Step 1 — Build Graph

```
v → u
```

Store dependencies.

---

## ✅ Step 2 — Calculate In-Degree

```
inDegree[x]
```

= number of prerequisites needed.

---

## ✅ Step 3 — Add Zero In-Degree Nodes

Courses with:

```
inDegree = 0
```

can be taken immediately.

---

## ✅ Step 4 — BFS Processing

Process course:

```
Remove it
Reduce neighbors inDegree
Add new zero inDegree nodes
```

---

## ✅ Step 5 — Cycle Detection

If processed courses:

```
count == numCourses
```

✅ No cycle

Else:

❌ Cycle exists

---

# 🧠 Dry Run Example

```
numCourses = 2
prerequisites = [[1,0]]
```

Graph:

```
0 → 1
```

InDegree:

```
[0,1]
```

Queue:
```
[0]
```

Process:

```
Take 0 → unlock 1
Take 1
```

Processed = 2 ✅

Return:
```
true
```

---

# ⏱ Time Complexity

```
O(V + E)
```

Where:

```
V = courses
E = prerequisites
```

---

# 📦 Space Complexity

```
O(V + E)
```

Graph + Queue + InDegree.

---

# 🔥 Pattern Used

Topological Sort  
BFS  
Cycle Detection in Directed Graph  

---

# 🏆 Interview Insight

Whenever problem says:

```
Dependency
Order
Schedule
Prerequisite
```

Think immediately:

```
Topological Sort
```

---

# ✅ Key Idea

```
Cycle present → cannot finish courses
No cycle → valid ordering exists
```

---
