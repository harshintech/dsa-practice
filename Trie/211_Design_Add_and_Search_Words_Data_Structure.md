# 🌲 Design Add and Search Words Data Structure (Trie + DFS)

---

## 📌 Problem

Design a data structure that supports:

```
addWord(word)
search(word)
```

Special Rule:

```
'.' can match ANY character
```

---

## 🧩 Example

```
addWord("bad")
addWord("dad")
addWord("mad")

search("pad") → false
search("bad") → true
search(".ad") → true
search("b..") → true
```

---

# 🚀 Core Idea

This problem is:

```
Trie + Backtracking (DFS)
```

Because:

```
'.' introduces multiple possible paths
```

Normal Trie search cannot handle this directly.

---

# 🧠 Trie Node Structure

Each node stores:

```
children[26] → next characters
eow          → end of word
```

---

# 💻 Full Code

```java
class WordDictionary {

    class Node {
        Node[] children = new Node[26];
        boolean eow = false;
    }

    Node root;

    public WordDictionary() {
        root = new Node();
    }

    public void addWord(String word) {

        Node curr = root;

        for(int i = 0; i < word.length(); i++) {

            int idx = word.charAt(i) - 'a';

            if(curr.children[idx] == null)
                curr.children[idx] = new Node();

            curr = curr.children[idx];
        }

        curr.eow = true;
    }

    public boolean search(String word) {
        return helper(word, 0, root);
    }

    private boolean helper(String word, int i, Node curr) {

        if(curr == null)
            return false;

        if(i == word.length())
            return curr.eow;

        char ch = word.charAt(i);

        // Normal character
        if(ch != '.') {
            int idx = ch - 'a';
            return helper(word, i + 1, curr.children[idx]);
        }

        // Wildcard '.'
        for(int k = 0; k < 26; k++) {
            if(helper(word, i + 1, curr.children[k]))
                return true;
        }

        return false;
    }
}
```

---

# 🔥 How Search Works

---

## ✅ Normal Character

Example:
```
search("bad")
```

Traversal:

```
b → a → d
```

Check:
```
eow == true
```

Return ✅

---

## ✅ Wildcard Case (`.`)

Example:
```
search(".ad")
```

Meaning:

```
?ad
```

Algorithm tries:

```
aad
bad
cad
dad
...
zad
```

DFS explores all valid branches.

---

# 🌳 Recursion Visualization

Searching:

```
".ad"
```

```
root
 ├─ a → ad ?
 ├─ b → ad ✅
 ├─ c → ad ?
 └─ ...
```

As soon as one path succeeds → return true.

---

# 🧠 Why DFS Needed?

Because:

```
'.' = branching decision
```

So search becomes:

```
Tree traversal problem
```

---

# ⏱ Time Complexity

---

### addWord

```
O(L)
```

---

### search

Worst case:

```
O(26^L)
```

(when many '.' exist)

Average case much faster.

---

# 📦 Space Complexity

```
O(N × L)
```

Where:

- N = number of words
- L = word length

---

# 🔥 Pattern Used

Trie  
DFS  
Backtracking  
Wildcard Matching  

---

# 🏆 Interview Insight

Whenever you see:

```
Dictionary + wildcard search
```

Think immediately:

```
Trie + DFS
```

---

# ⚠ Important Trick

Normal Trie:
```
single path traversal
```

Wildcard Trie:
```
multi-path recursion
```

---

# ✅ Summary

| Operation | Idea |
|---|---|
| addWord | Insert into Trie |
| search | DFS traversal |
| '.' | Try all children |

---

# 🚀 Real Interview Follow-ups

- Word Search II
- Regex Matching Lite
- Auto Suggest System
- File System Search

---

