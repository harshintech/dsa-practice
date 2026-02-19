# 🌲 Trie (Prefix Tree) — Complete Implementation

---

## 📌 What is Trie?

A **Trie** is a tree data structure used to store strings efficiently.

Main purpose:

✅ Fast word search  
✅ Prefix search  
✅ Dictionary problems  

---

## 🧠 Structure

Each node contains:

```
children[26] → next characters (a-z)
eow          → end of word flag
```

Example:

Insert words:

```
cat
car
dog
```

Trie structure:

```
        root
       /   \
      c     d
      |     |
      a     o
     / \     \
    t   r     g
```

---

# 🚀 Trie Operations

---

## ✅ 1. Insert Word

### Idea

Move character by character:

- Create node if missing
- Move pointer forward
- Mark last node as word end

---

### Code

```java
public void insert(String word) {
    Trie curr = this;

    for(int i = 0; i < word.length(); i++) {
        int idx = word.charAt(i) - 'a';

        if(curr.children[idx] == null) {
            curr.children[idx] = new Trie();
        }

        curr = curr.children[idx];
    }

    curr.eow = true;
}
```

---

## ✅ 2. Search Word

Check:

```
Does complete word exist?
```

---

### Code

```java
public boolean search(String word) {
    Trie curr = this;

    for(int i = 0; i < word.length(); i++) {
        int idx = word.charAt(i) - 'a';

        Trie node = curr.children[idx];

        if(node == null)
            return false;

        curr = node;
    }

    return curr.eow;
}
```

---

## ✅ 3. Starts With Prefix

Check only path existence.

No need for end-of-word.

---

### Code

```java
public boolean startsWith(String prefix) {
    Trie curr = this;

    for(int i = 0; i < prefix.length(); i++) {
        int idx = prefix.charAt(i) - 'a';

        Trie node = curr.children[idx];

        if(node == null)
            return false;

        curr = node;
    }

    return true;
}
```

---

# 🧩 Full Trie Class

```java
class Trie {

    Trie[] children;
    boolean eow;

    public Trie() {
        children = new Trie[26];
        eow = false;
    }

    public void insert(String word) {
        Trie curr = this;

        for(int i = 0; i < word.length(); i++) {
            int idx = word.charAt(i) - 'a';

            if(curr.children[idx] == null)
                curr.children[idx] = new Trie();

            curr = curr.children[idx];
        }

        curr.eow = true;
    }

    public boolean search(String word) {
        Trie curr = this;

        for(int i = 0; i < word.length(); i++) {
            int idx = word.charAt(i) - 'a';

            if(curr.children[idx] == null)
                return false;

            curr = curr.children[idx];
        }

        return curr.eow;
    }

    public boolean startsWith(String prefix) {
        Trie curr = this;

        for(int i = 0; i < prefix.length(); i++) {
            int idx = prefix.charAt(i) - 'a';

            if(curr.children[idx] == null)
                return false;

            curr = curr.children[idx];
        }

        return true;
    }
}
```

---

# ⏱ Complexity

Let:

```
L = word length
```

| Operation | Time |
|-----------|------|
| Insert | O(L) |
| Search | O(L) |
| Prefix | O(L) |

---

# 📦 Space Complexity

Worst case:

```
O(26 × N × L)
```

Where:

- N = number of words
- L = average length

---

# 🔥 Important Interview Insights

---

## ✅ Trie vs HashSet

| Feature | Trie | HashSet |
|---|---|---|
| Prefix search | ✅ Fast | ❌ Slow |
| Memory | Higher | Lower |
| Word lookup | O(L) | O(1) avg |

---

## ✅ Used In Problems

- Word Break
- Word Search II
- Auto Complete
- Dictionary Matching
- Replace Words
- Search Suggestions

---

# ⚠ Common Beginner Mistake

❌ Checking `eow` inside loop  
✅ Check only **after traversal**

Correct:
```
return curr.eow;
```

---

# 🏆 Pattern Recognition

If problem says:

```
Prefix
Dictionary
Search words repeatedly
```

👉 Use **Trie**

---

