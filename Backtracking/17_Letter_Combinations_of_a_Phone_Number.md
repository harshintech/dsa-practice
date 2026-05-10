# 📱 Letter Combinations of a Phone Number

---

## 📌 Problem

Given a string of digits from `2` to `9`, return all possible letter combinations based on the classic phone keypad.

---

## 📞 Phone Keypad Mapping

| Digit | Letters |
|------:|---------|
| 2 | abc |
| 3 | def |
| 4 | ghi |
| 5 | jkl |
| 6 | mno |
| 7 | pqrs |
| 8 | tuv |
| 9 | wxyz |

---

## ✅ Example

Input:

```text
digits = "23"
```

Output:

```text
["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

Because:

```text
2 → abc
3 → def
```

All combinations are:

```text
a × d,e,f
b × d,e,f
c × d,e,f
```

---

## ✅ Code (UNCHANGED)

```java
class Solution {
    public List<String> letterCombinations(String digits) {

        List<String> res = new ArrayList<>();

        if (digits == null || digits.length() == 0) {
            return res;
        }

        Map<Character, String> digitToLetters = new HashMap<>();
        digitToLetters.put('2', "abc");
        digitToLetters.put('3', "def");
        digitToLetters.put('4', "ghi");
        digitToLetters.put('5', "jkl");
        digitToLetters.put('6', "mno");
        digitToLetters.put('7', "pqrs");
        digitToLetters.put('8', "tuv");
        digitToLetters.put('9', "wxyz");

        backtrack(digits, 0, new StringBuilder(), res, digitToLetters);

        return res;
    }

     private void backtrack(String digits, int idx, StringBuilder comb, List<String> res, Map<Character, String> digitToLetters) {

        if(idx == digits.length()){
            res.add(comb.toString());
            return;
        }

        String letters = digitToLetters.get(digits.charAt(idx));
        for(char letter : letters.toCharArray()){
            comb.append(letter);
            backtrack(digits,idx+1,comb,res,digitToLetters);
            comb.deleteCharAt(comb.length() - 1);
        }
        
     }
}
```

---

# 🧠 Core Idea

For each digit:

1. Get all possible letters.
2. Try each letter.
3. Move to next digit.
4. Backtrack and try the next letter.

This is exactly a **depth-first search over all possible combinations**.

---

# 🎯 What This Problem Really Is

This problem is the **Cartesian Product** of letter groups.

For:

```text
"23"
```

We need:

```text
{a,b,c} × {d,e,f}
```

Backtracking systematically generates every possible path.

---

# 🌳 Recursion Tree for `"23"`

```text
                ""
          /      |      \
         a       b       c
      / | \   / | \   / | \
     d  e  f d  e  f d  e  f
```

Leaves:

```text
ad ae af bd be bf cd ce cf
```

---

# 🧩 Parameters Explained

```java
backtrack(digits, idx, comb, res, digitToLetters)
```

| Parameter | Meaning |
|---------:|---------|
| `digits` | Input digit string |
| `idx` | Current digit index |
| `comb` | Current partial combination |
| `res` | Final answer list |
| `digitToLetters` | Digit → letters mapping |

---

# 🛑 Base Case

```java
if(idx == digits.length())
```

We have chosen one letter for every digit.

So current combination is complete.

Save it:

```java
res.add(comb.toString());
```

---

# 🔄 Backtracking Step

For current digit:

```java
String letters = digitToLetters.get(digits.charAt(idx));
```

Try each letter:

```java
for(char letter : letters.toCharArray())
```

1. Add letter
2. Recurse to next digit
3. Remove letter

---

# ✏️ Why Use `StringBuilder`?

Strings are immutable in Java.

Using `StringBuilder` allows efficient:

- `append()`
- `deleteCharAt()`

Both are ideal for backtracking.

---

# 🧪 Dry Run (`digits = "23"`)

Start:

```text
idx = 0, comb = ""
letters = "abc"
```

Choose `'a'`:

```text
comb = "a"
```

Recurse to digit `'3'`:

```text
letters = "def"
```

Choose `'d'`:

```text
comb = "ad"
```

`idx == 2` → save `"ad"`

Backtrack:

```text
comb = "a"
```

Choose `'e'` → `"ae"`

Choose `'f'` → `"af"`

Backtrack to empty and repeat for `'b'` and `'c'`.

---

# ⏱ Complexity

Let:

- `n = digits.length()`
- each digit has at most 4 letters

### Time

```text
O(4^n × n)
```

- `4^n` combinations
- each combination length `n`

### Space

```text
O(n)
```

Recursion depth and current combination.

---

# 🏆 Interview Pattern Recognition

If problem asks for:

- All possible strings
- Character choices per position
- Generate every combination

Think:

```text
Backtracking / DFS / Cartesian Product
```

---

# 🔥 Golden Mental Model

```text
One digit = one level of recursion
One letter = one branch
Complete path = one answer
```

---
