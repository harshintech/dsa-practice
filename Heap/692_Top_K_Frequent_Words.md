# 🧠 Top K Frequent Words (Min Heap + Custom Comparator)

---

## 📌 Problem

Given an array of strings `words` and an integer `k`,  
return the `k` most frequent words.

### Sorting Rules:

1. Higher frequency first  
2. If frequencies are equal → lexicographically smaller word first  

---

## 🧩 Example

Input:
```
words = ["i","love","leetcode","i","love","coding"]
k = 2
```

Output:
```
["i","love"]
```

Because:

```
i → 2
love → 2
coding → 1
leetcode → 1
```

Same frequency (2), so lexicographically smaller comes first.

---

# 🚀 Approach (HashMap + Min Heap of Size K)

## 🔑 Key Idea

1️⃣ Count frequency using HashMap  
2️⃣ Use a Min Heap of size `k`  
3️⃣ Custom comparator handles:
   - Frequency ascending
   - If tie → reverse lexicographical order  
4️⃣ Reverse result at end  

---

# 💻 Java Code

```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {

        Map<String,Integer> map = new HashMap<>();

        // Step 1: Count frequency
        for(String word: words){
            map.put(word, map.getOrDefault(word, 0) + 1);
        }

        // Step 2: Min Heap with custom comparator
        PriorityQueue<String> minHeap =
            new PriorityQueue<>((a, b) -> {
                if (map.get(a).equals(map.get(b))) {
                    return b.compareTo(a);   // reverse lex order
                }
                return map.get(a) - map.get(b); // smaller freq first
            });

        // Step 3: Keep heap size = k
        for (String word : map.keySet()) {
            minHeap.add(word);

            if (minHeap.size() > k) {
                minHeap.poll();
            }
        }

        // Step 4: Build result
        List<String> res = new ArrayList<>();

        while(!minHeap.isEmpty()){
            res.add(minHeap.poll());
        }

        // Reverse because it's min heap
        Collections.reverse(res);

        return res;
    }
}
```

---

# 🎯 Why b.compareTo(a)?

When frequency is same:

We want lexicographically smaller word to stay.

But since it's a **min heap**,  
we remove the smallest element.

So we reverse comparison:

```
b.compareTo(a)
```

This ensures:

Lexicographically larger word gets removed first.

---

# 🧠 Dry Run Example

Input:
```
["i","love","leetcode","i","love","coding"]
k = 2
```

Frequency Map:
```
i → 2
love → 2
leetcode → 1
coding → 1
```

Heap keeps only top 2.

Final heap contains:
```
["i","love"]
```

After reverse:
```
["i","love"]
```

---

# ⏱ Time Complexity

```
O(n log k)
```

Where:
- n = number of unique words

---

# 📦 Space Complexity

```
O(n)
```

For frequency map.

---

# 🔥 Pattern Used

HashMap for frequency  
Min Heap of size k  
Custom Comparator  
Top K Pattern  

---

# 🏆 Why Reverse at End?

Min heap gives smallest element first.

But we want highest frequency first.

So we reverse final list.

---

# ⚠ Important Comparator Logic

Comparator rules:

```
1. Frequency ascending
2. If tie → reverse lexicographical
```

Because heap removes smallest first.

---

# ✅ Final Output

Input:
```
["i","love","leetcode","i","love","coding"], k=2
```

Output:
```
["i","love"]
```





