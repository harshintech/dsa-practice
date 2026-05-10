# ➕ Expression Add Operators

---

## 📌 Problem

Given:

- A numeric string `num`
- An integer `target`

Insert operators:

- `+`
- `-`
- `*`

between digits so that the expression evaluates to `target`.

Return all valid expressions.

---

## ✅ Example

Input:

```text
num = "123"
target = 6
```

Output:

```text
["1+2+3", "1*2*3"]
```

---

## ✅ Code (UNCHANGED)

```java
class Solution {
    public List<String> addOperators(String num, int target) {
        List<String> rst = new ArrayList<>();

        if (num == null || num.length() == 0) {
            return rst;
        }

        helper(rst, "", num, target, 0, 0, 0);
        return rst;
    }

    private void helper(List<String> rst, String path, String num,int target, int pos, long eval, long multed) {
        if (pos == num.length()) {
            if (target == eval) {
                rst.add(path);
            }
            return;
        }
       
        for (int i = pos; i < num.length(); i++) {
            if (i != pos && num.charAt(pos) == '0') {
                break;
            }

            long cur = Long.parseLong(num.substring(pos, i + 1));

            if (pos == 0) {
                helper(rst, path + cur, num, target,i + 1, cur, cur);
            } else {
                helper(rst, path + "+" + cur, num, target,i + 1, eval + cur, cur);
                helper(rst, path + "-" + cur, num, target,i + 1, eval - cur, -cur);
                helper(rst, path + "*" + cur, num, target,i + 1,eval - multed + multed * cur,multed * cur);
            }
        }
    }
}
```

---

# 🧠 Core Idea

This is a **Backtracking** problem.

At each step:

1. Pick the next number (could be multiple digits).
2. Insert one of:
   - `+`
   - `-`
   - `*`
3. Update expression value.
4. Recurse.

---

# 🧩 Parameters Explained

```java
helper(rst, path, num, target, pos, eval, multed)
```

| Parameter | Meaning |
|---------:|---------|
| `path` | Current expression string |
| `pos` | Current index in `num` |
| `eval` | Current evaluated value |
| `multed` | Last multiplied term |

---

# 🎯 Why `multed` Is Needed

Multiplication has higher precedence than addition/subtraction.

Example:

```text
1 + 2 * 3
```

Correct result:

```text
7
```

Not:

```text
9
```

So when we encounter `*`, we must undo the last term and replace it with the multiplied value.

---

# 🔥 The Most Important Formula

```java
eval - multed + multed * cur
```

---

## Example

Current expression:

```text
1 + 2
```

State:

```text
eval = 3
multed = 2
```

Now append:

```text
* 3
```

Correct expression:

```text
1 + 2 * 3 = 7
```

Calculation:

```text
eval - multed + multed * cur
= 3 - 2 + 2 * 3
= 1 + 6
= 7
```

---

# ➖ Why `multed = -cur` for Subtraction?

Expression:

```text
1 - 2
```

State:

```text
eval = -1
multed = -2
```

If later we append:

```text
* 3
```

Formula:

```text
-1 - (-2) + (-2 * 3)
= -1 + 2 - 6
= -5
```

Which matches:

```text
1 - 2 * 3 = -5
```

---

# 🚫 Leading Zero Handling

```java
if (i != pos && num.charAt(pos) == '0') {
    break;
}
```

Prevents invalid numbers such as:

```text
05
00
012
```

Only `"0"` is allowed.

---

# 🛑 Base Case

```java
if (pos == num.length())
```

All digits are used.

If:

```text
eval == target
```

Save the expression.

---

# 🌳 Example Walkthrough

Input:

```text
num = "123"
target = 6
```

Possible expressions:

```text
1+2+3 = 6 ✅
1*2*3 = 6 ✅
1+23 = 24
12-3 = 9
```

Result:

```text
["1+2+3", "1*2*3"]
```

---

# 🔄 First Number Special Case

```java
if (pos == 0)
```

The first number is added directly without any operator.

Example:

```text
path = "12"
eval = 12
multed = 12
```

---

# ⏱ Complexity

Let `n = num.length()`.

Worst case:

```text
O(4^n)
```

Because at each split we can choose:

- No split / longer number
- `+`
- `-`
- `*`

---

# 💾 Space Complexity

```text
O(n)
```

Recursion depth.

---

# 🏆 Pattern Recognition

If problem asks to:

- Generate expressions
- Track running value
- Handle operator precedence

Think:

```text
Backtracking + Expression Evaluation
```
