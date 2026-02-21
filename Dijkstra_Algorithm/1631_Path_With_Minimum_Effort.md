# 🧗 Minimum Effort Path (Dijkstra on Grid)

---

## 📌 Problem

You are given a matrix:

```
heights[i][j]
```

You must move from:

```
(0,0) → (m-1,n-1)
```

Allowed moves:

```
Up | Down | Left | Right
```

---

## 🎯 Goal

Minimize:

```
Maximum absolute height difference
between consecutive cells
```

NOT total sum ❌

BUT:

```
minimum possible maximum effort
```

---

## 🧠 Key Observation

Normal shortest path:

```
distance = SUM of weights
```

But here:

```
path cost = MAX edge weight
```

So we modify Dijkstra.

---

# 🔥 Core Idea

At every step:

```
Effort =
max(previous effort,
    height difference)
```

We always choose path having:

```
minimum effort so far
```

👉 Perfect use case of **Dijkstra Algorithm**

---

# 💻 Code

```java
class Solution {

    class Pair{
        int row,col,effort;

        public Pair(int r,int c,int e){
            row = r;
            col = c;
            effort = e;
        }
    }
    public int minimumEffortPath(int[][] heights) {
        
        int m = heights.length;
        int n = heights[0].length;

        int[][] dist = new int[m][n];

        for(int[] row : dist){
            Arrays.fill(row,Integer.MAX_VALUE);
        }

        PriorityQueue<Pair> pq = new PriorityQueue<>((a,b)-> a.effort - b.effort);
        pq.add(new Pair(0,0,0));
        dist[0][0] = 0;

        int[] dr = { -1, 1, 0, 0 };
        int[] dc = { 0, 0, -1, 1 };

        while(!pq.isEmpty()){
            
            Pair curr = pq.poll();

            int r = curr.row;
            int c = curr.col;
            int effort = curr.effort;

            //reached destination 
            if(r == m - 1 && c == n - 1){
                return effort;
            }

            for(int i = 0;i<4;i++){
                int nr = r + dr[i];
                int nc = c + dc[i];

                if(nr >= 0 && nc>=0 && nr<m && nc<n){
                    int newEffort = Math.max(
                        effort,
                        Math.abs(heights[r][c] - heights[nr][nc])
                    );

                    if(newEffort < dist[nr][nc]){
                        dist[nr][nc] = newEffort;
                        pq.add(new Pair(nr,nc,newEffort));
                    }
                }
            }
        }
         return 0;
    }
}
```

---

# 🌄 Graph Visualization

Grid becomes graph:

```
1   2   2
3   8   2
5   3   5
```

Each cell = node

Edges weight:

```
|height difference|
```

Example:

```
1 → 2 = 1
2 → 8 = 6
```

---

# 🚶 Path Comparison

### Path 1
```
1 → 2 → 2 → 2 → 5
max diff = 3
```

### Path 2
```
1 → 3 → 5 → 3 → 5
max diff = 2 ✅
```

Answer:

```
2
```

---

# ⚙️ Modified Dijkstra Logic

Normal:

```
newDist = dist + weight
```

Here:

```
newEffort =
max(currentEffort,
    edgeWeight)
```

---

# 🔄 Algorithm Flow

---

## Step 1
Start from:

```
(0,0)
effort = 0
```

---

## Step 2
Always pick cell with:

```
minimum effort
```

(using Min Heap)

---

## Step 3
Explore neighbours.

Update effort.

---

## Step 4
Stop immediately when destination reached ✅

(Dijkstra Property)

---

# ⏱ Complexity

### Time
```
O(M * N log(M*N))
```

Heap operations.

---

### Space
```
O(M * N)
```

Distance matrix.

---

# 🔥 Pattern Recognition

If problem says:

✅ Grid  
✅ Minimum maximum cost  
✅ Safest path  
✅ Effort / Risk / Capability  

👉 Think:

```
Modified Dijkstra
```

---

# 🏆 Golden Interview Insight

```
When path cost depends on MAX edge,
use Dijkstra with Math.max()
```

---

# 🚀 Advanced Note

This problem also solvable using:

✅ Binary Search + BFS  
✅ Union Find (Kruskal MST idea)

But Dijkstra = cleanest.

---

