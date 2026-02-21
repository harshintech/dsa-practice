# 🎓 Course Schedule II (Topological Sort Order)

---

## 📌 Problem

You are given:

```
numCourses
prerequisites
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
Valid order of courses
```

If impossible:

```
return empty array []
```

---

## 🧠 Core Idea

This problem asks:

```
Find ordering of nodes in Directed Graph
```

This is classic:

```
Topological Sorting
```

using

```
Kahn’s Algorithm (BFS)
```

---

# 🔗 Graph Representation

For prerequisite:

```
[u, v]
```

Create directed edge:

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
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        List<List<Integer>> graph = new ArrayList<>();

        for(int i = 0;i<numCourses;i++){
            graph.add(new ArrayList<>());
        }

        int[] inDegree = new int[numCourses];
        for(int i = 0;i<prerequisites.length;i++){
            int u = prerequisites[i][0];
            int v = prerequisites[i][1];
            
            graph.get(v).add(u);
            inDegree[u]++;
        }

        Queue<Integer> queue = new LinkedList<>();

        for(int i = 0;i<numCourses;i++){
            if(inDegree[i] == 0){
                queue.add(i);
            }
        }

        int completed = 0;
        int[] res = new int[numCourses];

        while(!queue.isEmpty()){
            int current = queue.poll();
            res[completed] =  current;
            completed++;

            for(int neighbour: graph.get(current)){
                inDegree[neighbour]--;
                if(inDegree[neighbour] == 0){
                    queue.add(neighbour);
                }
            }
        }

        if(completed != numCourses){
            return new int[0];
        }
        
        return res;
    }
}
```

---

# 🚀 Algorithm Steps

---

## ✅ Step 1 — Build Graph

```
v → u
```

Store dependency relation.

---

## ✅ Step 2 — Compute In-Degree

```
inDegree[i]
```

= number of prerequisites needed before taking course `i`.

---

## ✅ Step 3 — Add Independent Courses

Courses having:

```
inDegree = 0
```

can be taken immediately.

Add them to queue.

---

## ✅ Step 4 — BFS Processing

Repeat:

```
Take course
Add to result
Reduce neighbor indegree
Unlock next courses
```

---

## ✅ Step 5 — Cycle Check

If:

```
completed == numCourses
```

✅ Valid ordering exists

Else:

❌ Cycle present → impossible

---

# 🌳 Dry Run Example

```
numCourses = 4
prerequisites = [[1,0],[2,0],[3,1],[3,2]]
```

Graph:

```
0 → 1
0 → 2
1 → 3
2 → 3
```

---

### Initial InDegree

```
0 : 0
1 : 1
2 : 1
3 : 2
```

Queue:
```
[0]
```

---

### Process Flow

```
Take 0 → unlock 1,2
Queue → [1,2]

Take 1 → reduce 3
Take 2 → unlock 3

Take 3
```

---

✅ Result:

```
[0,1,2,3]
```

(or valid variation)

---

# ⏱ Complexity

### Time
```
O(V + E)
```

### Space
```
O(V + E)
```

---

# 🔥 Pattern Recognition

If problem says:

✅ order  
✅ dependency  
✅ scheduling  
✅ prerequisite  
✅ build sequence  

👉 Think instantly:

```
Topological Sort
```

---

# 🏆 Difference from Course Schedule I

| Problem | Output |
|------|------|
| Course Schedule I | true / false |
| Course Schedule II | actual ordering |

---

# ✅ Final Insight

```
Topological Sort =
Linear ordering of DAG
```

If cycle exists → ordering impossible.

---

