# LeetCode 567 - Permutation in String (Optimized Version)

---

## 📌 Problem

Given two strings `s1` and `s2`,  
return `true` if `s2` contains a permutation of `s1`.

A permutation means:
- Same characters
- Same frequency
- Order does not matter

---

## 🧩 Example

Input:
```
s1 = "ab"
s2 = "eidbaooo"
```

Output:
```
true
```

Because substring `"ba"` is a permutation of `"ab"`.

---

# 🚀 Approach (Sliding Window + Frequency Array)

## 🔑 Key Idea

Instead of using `HashMap`,  
we use two arrays of size 26:

- `map1` → frequency of s1
- `map2` → frequency of current window in s2

Since only lowercase letters exist,  
array size = 26.

We use a fixed-size sliding window of size `n`.

---

# 💡 Algorithm Steps

1. If `m < n` → return false.
2. Build frequency arrays for:
   - `s1`
   - First window of `s2`
3. Compare arrays.
4. Slide window:
   - Remove left character
   - Add new right character
5. Compare arrays after each slide.
6. If matched → return true.

---

# 💻 Java Code

```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {

        int n = s1.length();
        int m = s2.length();

        if (m < n)
            return false;

        int map1[] = new int[26];
        int map2[] = new int[26];

        for (int i = 0; i < n; i++) {
            map1[s1.charAt(i) - 'a']++;
            map2[s2.charAt(i) - 'a']++;
        }

        if (isMatched(map1, map2)) {
            return true;
        }

        for (int i = 1; i <= m - n; i++) {

            map2[s2.charAt(i - 1) - 'a']--;
            map2[s2.charAt(i + n - 1) - 'a']++;

            if (isMatched(map1, map2)) {
                return true;
            }
        }

        return false;
    }

    public boolean isMatched(int[] map1, int[] map2) {
        for (int i = 0; i < 26; i++) {
            if (map1[i] != map2[i]) {
                return false;
            }
        }
        return true;
    }
}
```

---

# 🎨 Graphical Representation

Example:

```
s1 = "ab"
s2 = "eidbaooo"
```

Window size = 2

---

### Step 1 → First Window

```
"ei"
map2 ≠ map1
```

---

### Slide Window

Remove 'e', Add 'd'

```
"id"
map2 ≠ map1
```

---

### Slide Again

Remove 'i', Add 'b'

```
"db"
map2 ≠ map1
```

---

### Slide Again

Remove 'd', Add 'a'

```
"ba"
map2 == map1 ✅
```

Return true.

---

# ⏱ Time Complexity

O(26 * (m - n))  
≈ O(m)

- Sliding window runs once.
- Each comparison checks 26 letters (constant).

---

# 📦 Space Complexity

O(1)

- Only two arrays of size 26 used.

---

# 🧠 Why This Is Better Than HashMap

✔ Faster lookup  
✔ No hashing overhead  
✔ Fixed-size array comparison  
✔ Cleaner and optimal for lowercase letters  

---

# 🔥 Pattern Used

Sliding Window  
Fixed Size Window  
Frequency Array  
Anagram Check  

---

# ✅ Final Output

Input:
```
s1 = "ab"
s2 = "eidbaooo"
```

Output:
```
true
```

---

# ⚡ Interview Tip

If interviewer asks optimization:

Instead of checking full 26 every time,
you can maintain a `matches` counter
to reduce comparison time further.




