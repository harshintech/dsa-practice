# 🔍 Word Search (Backtracking on Grid)

---

## 📌 Problem

Given:

```
board → 2D character grid
word  → string
```

Return:

```
true  → if word exists in grid
false → otherwise
```

Rules:

- Letters must be adjacent (up, down, left, right)
- Same cell cannot be used twice

---

## 🧩 Example

Input:

```
board =
[
 ['A','B','C','E'],
 ['S','F','C','S'],
 ['A','D','E','E']
]

word = "ABCCED"
```

Output:
```
true
```

---

# 🚀 Approach (DFS + Backtracking)

---

## 🔑 Core Idea

For each cell:

If it matches first character:

→ Start DFS

At each step:

1️⃣ Check boundary  
2️⃣ Check visited  
3️⃣ Check character match  
4️⃣ Explore 4 directions  
5️⃣ Backtrack if path fails  

---

# 💻 Java Code

```java
class Solution {
    public boolean exist(char[][] board, String word) {

        int m = board.length;
        int n = board[0].length;

        boolean[][] visited = new boolean[m][n];

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {

                if (board[i][j] == word.charAt(0)) {

                    if (backtrack(board, word,
                                  visited, i, j, 0)) {
                        return true;
                    }
                }
            }
        }

        return false;
    }

    private boolean backtrack(char[][] board,
                              String word,
                              boolean[][] visited,
                              int i,
                              int j,
                              int index) {

        if (index == word.length()) {
            return true;
        }

        if (i < 0 || i >= board.length ||
            j < 0 || j >= board[0].length ||
            visited[i][j] ||
            board[i][j] != word.charAt(index)) {
            return false;
        }

        visited[i][j] = true;

        boolean found =
            backtrack(board, word, visited,
                      i + 1, j, index + 1) ||
            backtrack(board, word, visited,
                      i - 1, j, index + 1) ||
            backtrack(board, word, visited,
                      i, j + 1, index + 1) ||
            backtrack(board, word, visited,
                      i, j - 1, index + 1);

        visited[i][j] = false; // backtrack

        return found;
    }
}
```

---

# 🧠 Why Backtracking?

We must:

```
Try path
If fails → undo (visited = false)
Try another path
```

Without undoing, other paths won’t work.

---

# 🌳 Recursion Tree Example

For word:

```
"AB"
```

From cell A:

```
   A
  /|\
 B ? ?
```

If B matches → success  
Else → backtrack  

---

# 🧠 Dry Run

Word: `"SEE"`

Start at:

```
(1,3) = 'S'
```

Explore neighbors:

```
(2,3) = 'E'
```

Next:

```
(2,2) = 'E'
```

Word found → return true.

---

# ⏱ Time Complexity

Worst case:

```
O(m × n × 4^L)
```

Where:

- m × n → starting positions
- L → word length

---

# 📦 Space Complexity

```
O(L)
```

Recursion stack depth.

---

# 🔥 Pattern Used

Backtracking  
DFS on Grid  
Visited Matrix  
4-Directional Traversal  

---

# 🏆 Similar Problems

- Number of Islands
- Word Search II
- Path in Matrix
- Rat in Maze

All use:

```
Grid + DFS + Backtracking
```

---

# ⚠ Important Insight

You must:

```
Mark visited BEFORE recursion
Unmark AFTER recursion
```

Otherwise:

Paths get blocked.

---

# ✅ Final Output

Input:
```
"ABCCED"
```

Output:
```
true
```

---


