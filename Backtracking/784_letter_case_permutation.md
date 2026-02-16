# LeetCode 784 - Letter Case Permutation (Backtracking)

---

## 📌 Problem

Given a string `s`,  
return all possible strings formed by:

```
Changing each letter to lowercase or uppercase.
```

Digits remain unchanged.

---

## 🧩 Example

Input:
```
s = "a1b2"
```

Output:
```
[
 "a1b2",
 "a1B2",
 "A1b2",
 "A1B2"
]
```

---

# 🚀 Approach (Backtracking on Character Array)

---

## 🔑 Core Idea

For every character:

If digit → only one choice  
If letter → two choices  
   - lowercase  
   - uppercase  

This naturally forms a recursion tree.

---

# 💻 Java Code

```java

 /**  
            a1b2   i=0, when it's at a, since it's a letter, we have two branches: a, A
         /        \
       a1b2       A1b2 i=1 when it's at 1, we only have 1 branch which is itself
        |          |   
       a1b2       A1b2 i=2 when it's at b, we have two branches: b, B
       /  \        / \
      a1b2 a1B2  A1b2 A1B2 i=3  when it's at 2, we only have one branch.
       |    |     |     |
      a1b2 a1B2  A1b2  A1B2 i=4 = S.length(). End recursion, add permutation to ans. 
      
      During this process, we are changing the S char array itself
*/

class Solution {
    public List<String> letterCasePermutation(String s) {

        List<String> result = new ArrayList<>();

        backtrack(s.toCharArray(), 0, result);

        return result;
    }

    private void backtrack(char[] arr,
                           int index,
                           List<String> result){

        // Base case
        if(index == arr.length){
            result.add(new String(arr));
            return;
        }

        if (Character.isDigit(arr[index])) {

            backtrack(arr, index + 1, result);

        } else {

            // Lowercase branch
            arr[index] =
                Character.toLowerCase(arr[index]);
            backtrack(arr, index + 1, result);

            // Uppercase branch
            arr[index] =
                Character.toUpperCase(arr[index]);
            backtrack(arr, index + 1, result);
        }
    }
}
```

---

# 🧠 Why Use `char[]`?

Because:

```
Strings are immutable.
```

Using `char[]` allows:

- Modify character in-place
- Avoid extra string creation

Efficient.

---

# 🌳 Recursion Tree Example

Input:
```
"a1b"
```

Tree:

```
          a
       /      \
      a        A
      |        |
      1        1
      |        |
      b        b
     / \      / \
    b   B    b   B
```

Total outputs:
```
4
```

---

# 🧠 Dry Run

Input:
```
"ab"
```

Start:
```
index = 0
```

Lowercase:
```
"a"
```

Uppercase:
```
"A"
```

Then next char:

Final:
```
["ab","aB","Ab","AB"]
```

---

# ⏱ Time Complexity

If string length = n

Worst case (all letters):

```
O(2^n)
```

Because each letter has 2 choices.

---

# 📦 Space Complexity

Recursion depth:
```
O(n)
```

Result storage:
```
O(2^n)
```

---

# 🔥 Pattern Used

Backtracking  
Binary Choice  
Character Transformation  

---

# 🏆 Similar Problems

- Subsets
- Permutations
- Generate Parentheses
- Combination Sum

All use:

```
Decision Tree Expansion
```

---

# ⚠ Important Insight

We do NOT need to revert case manually.

Because:

Each recursive branch overwrites it anyway.

---

# ✅ Final Output

Input:
```
"a1b2"
```

Output:
```
4 combinations
```

---

