# 🔁 Valid Palindrome II (At Most One Deletion)

---

## 📌 Problem

Given a string `s`, return:

```
true  → if it can become a palindrome
false → otherwise
```

You are allowed to delete **at most one character**.

---

## 🧩 Example

Input:
```
s = "abca"
```

Output:
```
true
```

Because removing `'b'` gives:

```
"aca"
```

Which is a palindrome.

---

# 🚀 Approach (Two Pointers)

---

## 🔑 Core Idea

Use two pointers:

```
left  → start
right → end
```

If characters match → move inward.

If mismatch occurs:

Try two possibilities:

1️⃣ Skip left character  
2️⃣ Skip right character  

If either works → return true.

---

# 💻 Java Code

```java
class Solution {
    public boolean validPalindrome(String s) {

        int left = 0;
        int right = s.length() - 1;

        while(left <= right){

            if(s.charAt(left) != s.charAt(right)){
                return isPalindrome(s, left + 1, right) ||
                       isPalindrome(s, left, right - 1);
            }

            left++;
            right--;
        }

        return true;
    }

    private boolean isPalindrome(String s,
                                 int left,
                                 int right){

        while(left < right){

            if(s.charAt(left) != s.charAt(right)){
                return false;
            }

            left++;
            right--;
        }

        return true;
    }
}
```

---

# 🧠 Why This Works

When mismatch occurs:

We are allowed only ONE deletion.

So we test both possibilities:

```
Delete left
Delete right
```

If either gives valid palindrome → answer is true.

---

# 🎯 Dry Run

Input:
```
"abca"
```

Compare:

```
a == a ✔
b != c ❌
```

Now check:

```
isPalindrome("bca") ❌
isPalindrome("abc") ❌
```

Actually correct check:

```
Skip left → check "ca" → valid?
Skip right → check "bc" → valid?
```

Correct branch:

Skip 'b':

```
"aca" → valid ✔
```

Return true.

---

# ⏱ Time Complexity

Worst case:

```
O(n)
```

We scan string once,  
and at most one extra palindrome check.

---

# 📦 Space Complexity

```
O(1)
```

No extra space.

---

# 🔥 Pattern Used

Two Pointers  
Greedy Local Fix  
Palindrome Checking  

---

# 🧠 Important Insight

We only allow:

```
One deletion.
```

So once mismatch happens,
we don't continue normal loop.
We immediately test both options.

---

# 🏆 Similar Problems

- Valid Palindrome I  
- Longest Palindromic Substring  
- Palindrome Linked List  

---

# ⚠ Small Note

Variable `delete = 1;` in your code  
is unused and unnecessary.

Logic already handles single deletion.

---

# ✅ Final Output

Input:
```
"abca"
```

Output:
```
true
```

---


