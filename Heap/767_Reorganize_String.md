# LeetCode 767 - Reorganize String (Max Heap + Greedy)

---

## 📌 Problem

Given a string `s`, rearrange the characters so that:

```
No two adjacent characters are the same
```

If not possible → return `""`.

---

## 🧩 Example

Input:
```
s = "aab"
```

Output:
```
"aba"
```

---

Input:
```
s = "aaab"
```

Output:
```
""
```

Because it is impossible to arrange without adjacent duplicates.

---

# 🚀 Approach (Greedy + Max Heap)

---

## 🔑 Step 1: Count Frequency

Count occurrences of each character.

---

## 🔑 Step 2: Check Impossible Condition

If the highest frequency:

```
max > (n + 1) / 2
```

Then it is impossible.

Why?

Because one character would dominate and force adjacency.

---

## 🔑 Step 3: Use Max Heap

Store:

```
[character_index, frequency]
```

Heap ordered by:

```
Highest frequency first
```

---

## 🔑 Step 4: Always Pick Top 2 Frequent Characters

Why 2?

Because:

If we always place two different highest frequency characters:

```
No adjacent duplicates happen.
```

After using them:

- Decrease frequency
- Put back into heap if still available

---

# 💻 Java Code

```java
class Solution {
    public String reorganizeString(String s) {

        int n = s.length();

        // Step 1: Count frequency
        int[] freq = new int[26];
        for (char ch : s.toCharArray()) {
            freq[ch - 'a']++;
        }

        // Step 2: Check impossible condition
        int max = 0;
        for (int f : freq) {
            max = Math.max(max, f);
        }

        if (max > (n + 1) / 2) {
            return "";
        }

        // Step 3: Max Heap based on frequency
        PriorityQueue<int[]> pq =
            new PriorityQueue<>((a, b) -> b[1] - a[1]);

        for (int i = 0; i < 26; i++) {
            if (freq[i] > 0) {
                pq.offer(new int[] { i, freq[i] });
            }
        }

        StringBuilder sb = new StringBuilder();

        // Step 4: Take two most frequent each time
        while (pq.size() > 1) {

            int[] first = pq.poll();
            int[] second = pq.poll();

            sb.append((char)(first[0] + 'a'));
            sb.append((char)(second[0] + 'a'));

            first[1]--;
            second[1]--;

            if (first[1] > 0)
                pq.offer(first);
            if (second[1] > 0)
                pq.offer(second);
        }

        // If one element left
        if (!pq.isEmpty()) {
            sb.append((char)(pq.poll()[0] + 'a'));
        }

        return sb.toString();
    }
}
```

---

# 🎯 Why Pick Two At A Time?

If you pick only one:

```
aaaab
```

You might accidentally place two same letters together.

But picking top 2 ensures:

```
We alternate highest frequencies.
```

---

# 🧠 Dry Run

Input:
```
s = "aab"
```

Frequency:
```
a = 2
b = 1
```

Heap:
```
[a(2), b(1)]
```

Step:

```
Take a, b → "ab"
a becomes 1
```

Remaining:
```
a(1)
```

Append:
```
"aba"
```

---

# ⏱ Time Complexity

Let:

```
n = length of string
```

Heap operations:

```
O(n log 26)
```

Since max 26 letters:

```
O(n)
```

---

# 📦 Space Complexity

```
O(26)
```

Constant.

---

# 🔥 Pattern Used

Greedy  
Max Heap  
Frequency Distribution  

---

# ⚠ Important Insight

Condition:

```
max > (n + 1) / 2
```

Is necessary and sufficient.

If it passes, solution always exists.

---

# 🏆 Interview Insight

This problem combines:

- Heap
- Greedy
- Frequency balancing
- Scheduling pattern (similar to Task Scheduler)

Very common FAANG medium.

---

# ✅ Final Output

Input:
```
"aab"
```

Output:
```
"aba"
```

Input:
```
"aaab"
```

Output:
```
""
```

