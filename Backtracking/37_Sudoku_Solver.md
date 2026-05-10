# 🧩 Sudoku Solver

---

## 📌 Problem

Given a partially filled Sudoku board, fill all empty cells (`'.'`) so that:

- Each row contains digits `1` to `9` exactly once.
- Each column contains digits `1` to `9` exactly once.
- Each `3 × 3` subgrid contains digits `1` to `9` exactly once.

---

## 🎯 Goal

Modify the board in-place to produce one valid Sudoku solution.

---

## ✅ Code (UNCHANGED)

```java
class Solution {
    private boolean isSafe(char[][] board, int row, int col, int number) {
        //row && column
        for (int i = 0; i < board.length; i++) {
            if (board[i][col] == (char) (number + '0')) {
                return false;
            }
            if (board[row][i] == (char) (number + '0')) {
                return false;
            }
        }

        //grid
        int sr = (row / 3) * 3;
        int sc = (col / 3) * 3;

        for (int i = sr; i < sr + 3; i++) {
            for (int j = sc; j < sc + 3; j++) {
                if (board[i][j] == (char) (number + '0')) {
                    return false;
                }
            }
        }

        return true;
    }

    private boolean helper(char[][] board, int row, int col) {

        if (row == board.length) {
            return true;
        }

        int nrow = 0;
        int ncol = 0;
        if (col != board.length - 1) {
            nrow = row;
            ncol = col + 1;
        } else {
            nrow = row + 1;
            ncol = 0;
        }

        if (board[row][col] != '.') {
            if (helper(board, nrow, ncol)) {
                return true;
            }
        } else {
            for (int i = 1; i <= 9; i++) {
                if (isSafe(board, row, col, i)) {
                    board[row][col] = (char) (i + '0');
                    if (helper(board, nrow, ncol)) {
                        return true;
                    } else {
                        board[row][col] = '.';
                    }
                }
            }
        }
        return false;
    }

    public void solveSudoku(char[][] board) {
        helper(board, 0, 0);
    }
}
```

---

# 🧠 Core Backtracking Idea

For each cell:

1. If already filled → move to next cell.
2. If empty:
   - Try digits `1` to `9`.
   - If safe, place the digit.
   - Recurse to next cell.
   - If recursion fails, remove the digit (backtrack).

---

# 🧭 Board Traversal Logic

The solver processes cells in row-major order:

```text
(0,0) → (0,1) → ... → (0,8)
                         ↓
(1,0) → (1,1) → ... → (1,8)
                         ↓
...
(8,8)
```

---

## Next Cell Calculation

```java
if (col != board.length - 1) {
    nrow = row;
    ncol = col + 1;
} else {
    nrow = row + 1;
    ncol = 0;
}
```

If not at the last column, move right.  
Otherwise, go to the first column of the next row.

---

# 🛑 Base Case

```java
if (row == board.length)
    return true;
```

When `row == 9`, we moved past the last row.

That means:

- All cells are validly filled.
- Sudoku is solved.

---

# 🔍 `isSafe()` Validation

Before placing a number, we ensure it does not already appear in:

1. The same row
2. The same column
3. The same `3 × 3` box

---

## 1️⃣ Row and Column Check

```java
for (int i = 0; i < board.length; i++)
```

Checks:

- `board[i][col]` → column
- `board[row][i]` → row

---

## 2️⃣ 3×3 Grid Check

### Starting Cell of Box

```java
int sr = (row / 3) * 3;
int sc = (col / 3) * 3;
```

This computes the top-left corner of the corresponding box.

---

### Example

For:

```text
row = 5, col = 7
```

```text
sr = (5 / 3) * 3 = 3
sc = (7 / 3) * 3 = 6
```

So the box starts at:

```text
(3, 6)
```

---

# 🔄 Backtracking Process

When a valid number is found:

```java
board[row][col] = (char)(i + '0');
```

Then recurse.

If recursion fails:

```java
board[row][col] = '.';
```

Undo the placement and try the next number.

---

# 🌳 Recursion Tree (Simplified)

```text
Empty cell
 ├── Try 1
 │    └── recurse
 ├── Try 2
 │    └── recurse
 ├── Try 3
 │    └── recurse
 ...
 └── Try 9
```

Only one successful branch is needed.

---

# 🔢 Character Conversion

```java
(char)(number + '0')
```

Converts integer `5` to character `'5'`.

Because:

```text
'0' = ASCII 48
5 + 48 = 53 = '5'
```

---

# ⏱ Complexity

Worst case:

```text
O(9^(number of empty cells))
```

Because each empty cell may try up to 9 digits.

In practice, pruning makes it much faster.

---

# 💾 Space Complexity

```text
O(number of empty cells)
```

Recursion stack.

---

# 🏆 Pattern Recognition

If problem asks to:

- Fill a board under constraints
- Try values
- Undo invalid choices

Think:

```text
Backtracking + Constraint Checking
```

---

# 🔥 Golden Mental Model

```text
Visit each cell
Try all valid digits
Move forward
If stuck, undo and try another digit
```
