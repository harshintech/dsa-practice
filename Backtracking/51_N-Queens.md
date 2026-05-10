# 👑 N-Queens

---

## 📌 Problem

Place `n` queens on an `n × n` chessboard such that:

- No two queens attack each other.

A queen can attack in:

- Same row
- Same column
- Upper-left / lower-right diagonal
- Upper-right / lower-left diagonal

---

## 🎯 Goal

Return all valid board configurations.

---

## ✅ Code (UNCHANGED)

```java
class Solution {

    private boolean isSafe(char[][] board,int row,int col,int n){
        //check same column upwards
        for(int i = row - 1;i>=0;i--){
            if(board[i][col] == 'Q'){
                return false;
            }
        }

        //check uper-left diagonal
        for(int i = row - 1,j = col - 1;i>=0 && j >= 0; i--, j--){
            if(board[i][j] == 'Q'){
                return false;
            }
        }

        //check upper-right diagonal
        for(int i = row - 1, j = col + 1; i>=0 && j<n; i--, j++){
            if(board[i][j] == 'Q'){
                return false;
            }
        }

        return true;
    }


    private void nQueens(char[][] board,int row,int n,List<List<String>> ans){
        if(row == n){
            List<String> temp = new ArrayList<>();

            for(int i = 0;i < n;i++){
                temp.add(new String(board[i]));
            }

            ans.add(temp);
            return;
        }

        for(int col = 0;col < n;col++){
            if(isSafe(board,row,col,n)){
                board[row][col] = 'Q';
                nQueens(board,row + 1,n,ans);
                board[row][col] ='.';
            }
        }
    }

    public List<List<String>> solveNQueens(int n) {
        List<List<String>> ans = new ArrayList<>();

        //create board
        char[][] board = new char[n][n];

        //fill board with '.'
        for(int i = 0;i < n;i++){
            Arrays.fill(board[i],'.');
        }

        nQueens(board, 0, n, ans);
        return ans;
    }
}
```

---

# 🧠 Core Backtracking Idea

We place exactly **one queen per row**.

So recursion parameter:

```text
row
```

represents:

> "Which row am I currently trying to fill?"

---

# 🎯 Why We Place One Queen Per Row

Since each recursive call handles one row:

- Row conflicts are automatically avoided.
- We only need to check:
  - Same column
  - Upper-left diagonal
  - Upper-right diagonal

---

# 🔥 Why Only UPPER Directions Are Checked

At row `r`, queens are already placed only in rows:

```text
0 to r-1
```

Rows below `r` are still empty.

Therefore:

- No need to check downward.
- Only upward positions can contain queens.

---

# 🔍 `isSafe()` Checks

---

## 1️⃣ Same Column

```java
for(int i = row - 1;i>=0;i--)
```

Checks all cells above in the same column.

---

## 2️⃣ Upper-Left Diagonal

```java
for(int i = row - 1,j = col - 1; i>=0 && j>=0; i--, j--)
```

Move diagonally up-left.

---

## 3️⃣ Upper-Right Diagonal

```java
for(int i = row - 1, j = col + 1; i>=0 && j<n; i--, j++)
```

Move diagonally up-right.

---

# 🧩 Backtracking Flow

For current row:

1. Try every column.
2. Check if safe.
3. Place queen.
4. Recurse to next row.
5. Remove queen (backtrack).

---

# 🛑 Base Case

```java
if(row == n)
```

All rows are filled.

We convert the board into `List<String>` and save it.

---

# 🌳 Recursion Tree (n = 4)

```text
row 0
 ├── col 0
 │    ├── row 1 ...
 ├── col 1
 │    ├── row 1 ...
 ├── col 2
 └── col 3
```

Each branch represents one queen placement.

---

# 👑 Example Solution (n = 4)

```text
.Q..
...Q
Q...
..Q.
```

---

# 🔄 Why Backtracking Works

When a placement leads to no valid solution:

```java
board[row][col] = '.';
```

We undo the move and try the next column.

---

# ⏱ Complexity

### Time

Worst case:

```text
O(N!)
```

Each row chooses among remaining columns.

### Space

```text
O(N²)
```

Board storage.

Recursion stack:

```text
O(N)
```

---

# 🏆 Pattern Recognition

If problem asks to:

- Place items under constraints
- Generate all valid configurations
- Try → recurse → undo

Think:

```text
Backtracking
```

---

# 🔥 Golden Mental Model

```text
One row = one recursion level
One column choice = one branch
Safe placement = continue
Unsafe placement = skip
All rows filled = one answer
```
