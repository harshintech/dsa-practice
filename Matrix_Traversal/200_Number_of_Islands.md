# 🧠 Number of Islands

---

## 📌 Problem

Given a 2D grid of `'1'`s (land) and `'0'`s (water),  
return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically.

---

## 🧩 Example

Input:

```
grid =
[
  ['1','1','0','0','0'],
  ['1','1','0','0','0'],
  ['0','0','1','0','0'],
  ['0','0','0','1','1']
]
```

Output:
```
3
```

---

# 🚀 Approach (DFS – Flood Fill)

## 🔑 Key Idea

- Traverse the grid.
- Whenever you find `'1'`, that means:
  - New island found.
- Use DFS to mark the entire island as visited.
- Increase island count.

We mark visited land as `'0'` to avoid revisiting.

---

# 💻 Java Code

```java
class Solution {
    public int numIslands(char[][] grid) {

        if(grid == null || grid.length == 0 || grid[0].length == 0){
            return 0;
        }

        int count = 0;

        for(int i = 0; i < grid.length; i++){
            for(int j = 0; j < grid[0].length; j++){

                if(grid[i][j] == '1'){
                    dfs(grid, i, j);
                    count++;
                }
            }
        }

        return count;
    }

    public void dfs(char[][] grid, int row, int col){

        // Boundary + water check
        if(row < 0 || row >= grid.length ||
           col < 0 || col >= grid[0].length ||
           grid[row][col] == '0'){
            return;
        }

        // Mark visited
        grid[row][col] = '0';

        // Explore 4 directions
        dfs(grid, row + 1, col);
        dfs(grid, row - 1, col);
        dfs(grid, row, col + 1);
        dfs(grid, row, col - 1);
    }
}
```

---

# 🎨 Step-by-Step Explanation

Grid:

```
1 1 0 0 0
1 1 0 0 0
0 0 1 0 0
0 0 0 1 1
```

---

### Step 1

Find first `'1'`

Call DFS → mark entire island as `'0'`

Grid becomes:

```
0 0 0 0 0
0 0 0 0 0
0 0 1 0 0
0 0 0 1 1
```

Island count = 1

---

### Step 2

Find next `'1'`

Mark it.

Island count = 2

---

### Step 3

Find next group:

```
1 1
```

Mark both.

Island count = 3

---

# ⏱ Time Complexity

O(m × n)

- Each cell visited once.

---

# 📦 Space Complexity

O(m × n) worst case

- Recursion stack in worst case (all land).

---

# 🧠 Why This Works

Each DFS call:

- Visits entire connected land.
- Prevents double counting.
- Counts each island exactly once.

---

# 🔥 Pattern Used

DFS  
Flood Fill  
Grid Traversal  
Connected Components  

---

# ⚡ Alternative

You can also solve using:

- BFS (Queue)
- Union-Find (Disjoint Set)

But DFS is simplest.

---

# ✅ Final Output

Input:
```
grid as above
```

Output:
```
3
```

---

# 🏆 Interview Tip

Always:

1. Check boundaries first.
2. Mark visited immediately.
3. Explore all 4 directions.


