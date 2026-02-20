# 🔍 Search Suggestions System (Trie)

---

## 📌 Problem

Given:

```
products[]  → list of product names
searchWord  → typed word
```

After typing **each character**, return:

```
Top 3 lexicographically smallest products
starting with current prefix
```

---

## 🧩 Example

Input:

```
products = ["mobile","mouse","moneypot","monitor","mousepad"]
searchWord = "mouse"
```

Output:

```
[
 ["mobile","moneypot","monitor"],
 ["mobile","moneypot","monitor"],
 ["mouse","mousepad"],
 ["mouse","mousepad"],
 ["mouse","mousepad"]
]
```

---

# 🚀 Approach — Trie + Prefix Suggestions

---

## 🔑 Core Idea

We build a **Trie**.

Each Trie node stores:

```
children[26]
suggestions (max 3 words)
```

So whenever we reach a prefix node,
we already have best suggestions ready.

---

# 🧠 Why Sort First?

```java
Arrays.sort(products);
```

Sorting guarantees:

```
Lexicographically smallest words inserted first
```

So Trie automatically keeps correct top-3 results.

---

# 🌲 Trie Node Structure

```java
class TrieNode {
    TrieNode[] children = new TrieNode[26];
    List<String> suggestions = new ArrayList<>();
}
```

Each node represents a prefix.

Example:

```
Prefix: "mo"
Suggestions:
["mobile","moneypot","monitor"]
```

---

# 💻 Code

```java
class Solution {

    class TrieNode {
        TrieNode[] children = new TrieNode[26];
        List<String> suggestions = new ArrayList<>();
    }

    TrieNode root = new TrieNode();

    void insert(String word) {

        TrieNode node = root;

        for(char ch : word.toCharArray()) {

            int idx = ch - 'a';

            if(node.children[idx] == null)
                node.children[idx] = new TrieNode();

            node = node.children[idx];

            if(node.suggestions.size() < 3)
                node.suggestions.add(word);
        }
    }

    public List<List<String>> suggestedProducts(
            String[] products,
            String searchWord) {

        Arrays.sort(products);

        for(String product : products)
            insert(product);

        List<List<String>> res = new ArrayList<>();

        TrieNode node = root;

        for(char ch : searchWord.toCharArray()) {

            int idx = ch - 'a';

            if(node != null)
                node = node.children[idx];

            if(node == null)
                res.add(new ArrayList<>());
            else
                res.add(node.suggestions);
        }

        return res;
    }
}
```

## Simple Solution (Recommanded For Only Size is small like here is 3)
```
class Solution {
    public List<List<String>> suggestedProducts(String[] products, String searchWord) {

        Arrays.sort(products);

        List<List<String>> res = new ArrayList<>();
        String prefix = "";

        for(char ch : searchWord.toCharArray()) {

            prefix += ch;
            List<String> list = new ArrayList<>();

            for(String product : products) {
                if(product.startsWith(prefix)) {
                    list.add(product);
                    if(list.size() == 3) break;
                }
            }

            res.add(list);
        }

        return res;
    }
}
```

---

# 🌳 Trie Visualization

Products:

```
mobile
moneypot
monitor
mouse
mousepad
```

Trie path:

```
m
└── o
    ├── b → mobile
    ├── n → moneypot
    ├── n → monitor
    └── u → mouse → mousepad
```

Each node stores **top 3 suggestions**.

---

# 🧠 Search Flow

Typing:

```
m
mo
mou
mous
mouse
```

Traversal:

```
root → m → mo → mou → mous → mouse
```

At each step:
```
return stored suggestions
```

---

# ⏱ Complexity

---

## Build Trie

```
O(N × L)
```

N = products  
L = word length

---

## Search

```
O(searchWord length)
```

Very fast lookup ✅

---

# 📦 Space Complexity

```
O(N × L)
```

Trie storage.

---

# 🔥 Why Trie Is Powerful Here?

Without Trie:

```
Every prefix → scan all products
```

Cost:
```
O(N × L × searchLen)
```

With Trie:

```
Direct prefix jump
```

Cost:
```
O(searchLen)
```

---

# 🆚 Simple Approach (Brute Force)

```java
product.startsWith(prefix)
```

Works but slower.

Trie = optimized solution.

---

# 🏆 Pattern Used

Trie  
Prefix Search  
Auto-complete System  

---

# 🧠 Real World Usage

- Amazon search
- Google autocomplete
- YouTube suggestions
- IDE code completion

---

# ⚠ Important Insight

Store suggestions **during insertion**, not search.

👉 Makes query extremely fast.

---

# ✅ Final Output

For `"mouse"`:

```
[
 ["mobile","moneypot","monitor"],
 ["mobile","moneypot","monitor"],
 ["mouse","mousepad"],
 ["mouse","mousepad"],
 ["mouse","mousepad"]
]
```

---

