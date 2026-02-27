# 🧩 Valid Sudoku — Logic Explanation

---

## 📌 Problem

Check whether a given **9 × 9 Sudoku board** is valid.

Rules:

✅ Each row → numbers 1–9 appear once  
✅ Each column → numbers 1–9 appear once  
✅ Each 3×3 box → numbers 1–9 appear once  

`.` means empty cell → ignore it.

---

## ✅ Code (UNCHANGED)

```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        int[][] rows = new int[9][9];
        int[][] cols = new int[9][9];
        int[][] boxes = new int[9][9];

        for(int r = 0;r < 9;r++){
            for(int c = 0;c < 9;c++){
                if(board[r][c] == '.'){
                    continue;
                }

                int val = board[r][c] - '1';

                if(rows[r][val] == 1){
                    return false;
                }

                rows[r][val] = 1;

                if(cols[c][val] == 1){
                    return false;
                }

                cols[c][val] = 1;

                int boxIdx = 3 * (r/3) + (c/3);

                if(boxes[boxIdx][val] == 1){
                    return false;
                }

                boxes[boxIdx][val]  = 1;
            }
        }

        return true;
    }
}
```

---

# 🧠 Core Idea

Instead of checking repeatedly,

we **remember what numbers already appeared**.

We track three things:

```
rows   → number already used in row
cols   → number already used in column
boxes  → number already used in 3×3 box
```

---

# ✅ Why Arrays Size = `[9][9]`

Sudoku:

```
9 rows
9 columns
Numbers 1 → 9
```

So:

```
rows[ row ][ number ]
cols[ col ][ number ]
boxes[ box ][ number ]
```

---

# 🔢 Character → Number Conversion

Board stores characters:

```
'1', '2', '3' ... '9'
```

We convert into index:

```java
int val = board[r][c] - '1';
```

---

### ASCII Trick

| Character | ASCII |
|-----------|------|
| '1' | 49 |
| '5' | 53 |

Example:

```
'5' - '1'
= 53 - 49
= 4
```

So:

```
'1' → index 0
'9' → index 8
```

Perfect for array indexing ✅

---

# ✅ Row Validation

Check:

```java
if(rows[r][val] == 1)
```

Meaning:

👉 This number already exists in this row.

Duplicate found ❌

Otherwise mark:

```java
rows[r][val] = 1;
```

---

# ✅ Column Validation

Same logic:

```java
if(cols[c][val] == 1)
```

Number already used in column ❌

---

# 🔥 MOST IMPORTANT PART  
## ✅ 3×3 Box Calculation

Sudoku has:

```
9 boxes total
```

Layout:

```
0 | 1 | 2
---------
3 | 4 | 5
---------
6 | 7 | 8
```

We must convert `(row, col)` → box index.

---

## ⭐ Formula

```java
int boxIdx = 3 * (r/3) + (c/3);
```

---

## 🧠 Why This Works

### Step 1 — Row Group

```
r/3 gives box row
```

Rows:

```
0,1,2 → 0
3,4,5 → 1
6,7,8 → 2
```

---

### Step 2 — Column Group

```
c/3 gives box column
```

Columns:

```
0,1,2 → 0
3,4,5 → 1
6,7,8 → 2
```

---

### Step 3 — Combine

```
boxIndex =
(rowGroup * 3) + columnGroup
```

---

## ✅ Example

Cell:

```
r = 4
c = 7
```

```
r/3 = 1
c/3 = 2
```

```
boxIdx = 3*1 + 2 = 5
```

Correct box ✅

---

# 🎯 Full Validation Flow

For every filled cell:

```
Check row duplicate
Check column duplicate
Check box duplicate
```

If any duplicate found → ❌ INVALID

Otherwise mark presence.

---

# ⏱ Complexity

### Time
```
O(9 × 9) = O(1)
```

Constant size board.

---

### Space
```
O(1)
```

Fixed arrays.

---

# 🚀 Interview Insight

This problem teaches:

✅ Hashing using arrays  
✅ Constraint tracking  
✅ Matrix indexing  
✅ Box mapping trick  

---

# 🏆 Golden Memory Trick

```
Row → r
Col → c
Box → 3*(r/3) + (c/3)
```

Memorize this once → Sudoku solved forever 🔥

---

If you want next:

✅ Sudoku Solver (Hard) intuition  
✅ Bitmask optimization version  
✅ Why boolean[][] faster than HashSet  

Just say 🚀


