# 🧠 Number of Closed Islands

---

## 📌 Problem

Given a 2D grid consisting of:

- `0` → land  
- `1` → water  

Return the number of **closed islands**.

A closed island is completely surrounded by water on all 4 sides  
and does NOT touch the boundary of the grid.

---

## 🧩 Example

Input:

```
grid =
[
 [1,1,1,1,1,1,1,0],
 [1,0,0,0,0,1,1,0],
 [1,0,1,0,1,1,1,0],
 [1,0,0,0,0,1,0,1],
 [1,1,1,1,1,1,1,0]
]
```

Output:
```
2
```

---

# 🚀 Approach (DFS + Boundary Check)

## 🔑 Key Idea

- Traverse only inner cells (ignore boundary).
- If we find land (`0`):
  - Use DFS to check whether island is closed.
- If during DFS we touch boundary → not closed.
- Otherwise → closed island.

---

# 💻 Java Code

```java
class Solution {

    public int closedIsland(int[][] grid) {

        int closedIsland = 0;

        for(int i = 1; i < grid.length - 1; i++){
            for(int j = 1; j < grid[0].length - 1; j++){

                if(grid[i][j] == 0){
                    if(isClosed(grid, i, j)){
                        closedIsland++;
                    }
                }
            }
        }

        return closedIsland;
    }

    public boolean isClosed(int[][] grid, int row, int col){

        // If out of boundary → not closed
        if(row < 0 || row >= grid.length ||
           col < 0 || col >= grid[0].length){
            return false;
        }

        // Water means safe boundary
        if(grid[row][col] == 1){
            return true;
        }

        // Mark visited
        grid[row][col] = 1;

        boolean down  = isClosed(grid, row + 1, col);
        boolean up    = isClosed(grid, row - 1, col);
        boolean right = isClosed(grid, row, col + 1);
        boolean left  = isClosed(grid, row, col - 1);

        return down && up && right && left;
    }
}
```

---

# 🎨 How It Works

Imagine:

```
0 0 0
0 1 0
0 0 0
```

If land touches boundary → DFS will go out of bounds → return false.

So island is NOT closed.

---

Example of closed island:

```
1 1 1
1 0 1
1 1 1
```

DFS never touches boundary → returns true.

---

# ⏱ Time Complexity

O(m × n)

- Each cell visited once.

---

# 📦 Space Complexity

O(m × n) worst case

- Recursion stack.

---

# 🧠 Important Trick

This line is key:

```
return down && up && right && left;
```

If ANY direction touches boundary → whole island becomes open.

---

# 🔥 Pattern Used

DFS  
Flood Fill  
Boundary Detection  
Connected Components  

---

# 🏆 Interview Insight

Difference between:

- Number of Islands → just count
- Closed Islands → must ensure not touching boundary

---

# ✅ Final Output

Input:
```
grid as above
```

Output:
```
2
```

