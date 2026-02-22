# 🧺 Merge Similar Items

---

## 📌 Problem

You are given two arrays:

```
items1 = [[value, weight]]
items2 = [[value, weight]]
```

Each item contains:

```
value  → item type
weight → item weight
```

---

## 🎯 Goal

Merge both arrays such that:

✅ Same values are combined  
✅ Weights are summed  
✅ Result sorted by value  

---

## ✅ Example

Input:

```
items1 = [[1,1],[4,5]]
items2 = [[3,2],[4,1]]
```

Output:

```
[[1,1],[3,2],[4,6]]
```

Because:

```
value 4 → 5 + 1 = 6
```




---

# ✅ Approach 1 — TreeMap (Ordered Map Not Recommanded ❌)

---

## 🧠 Idea

TreeMap automatically keeps keys sorted.

So:

```
No sorting needed later
```

---

## 💻 Code 

```java
class Solution {
    public List<List<Integer>> mergeSimilarItems(int[][] items1, int[][] items2) {

        TreeMap<Integer, Integer> map = new TreeMap<>();
        List<List<Integer>> res = new ArrayList<>();

        for (int i = 0; i < items1.length; i++) {
            map.put(items1[i][0], items1[i][1]);
        }

        for (int i = 0; i < items2.length; i++) {
            map.put(items2[i][0], map.getOrDefault(items2[i][0], 0) + items2[i][1]);
        }

         // convert map to result
        for (int key : map.keySet()) {
            res.add(Arrays.asList(key, map.get(key)));
        }

        return res;
    }
}
```

---

## ⏱ Complexity

```
Time  : O(N log N)
Space : O(N)
```

(Tree balancing)


---
# ✅ Approach 2 — HashMap + Sorting (Optimal)

---

## 🧠 Idea

1. Store value → weight in HashMap
2. Add weights if value repeats
3. Convert map → list
4. Sort by value


## 💻 Code 

```java
class Solution {
    public List<List<Integer>> mergeSimilarItems(int[][] items1, int[][] items2) {
        HashMap<Integer, Integer> hashMap = new HashMap<>();
        for(int[] array : items1) {
            int value = array[0];
            int weight = array[1];
            hashMap.put(value, weight);
        }

        for(int[] array : items2) {
            int value = array[0];
            int weight = array[1];
            hashMap.put(value, hashMap.getOrDefault(value, 0) + weight);
        }

        List<List<Integer>> list = new ArrayList<>();
        for(Map.Entry<Integer, Integer> map : hashMap.entrySet()) {
            list.add(new ArrayList<>(Arrays.asList(map.getKey(), map.getValue())));

        }
        
        list.sort((a, b) -> a.get(0) - b.get(0));

        return list;
    }
}
```

---

## ⏱ Complexity

```
Time  : O(N log N)
Space : O(N)
```

(sort required)


---


# ✅ Approach 3 — Frequency Array (MOST OPTIMAL 🚀)

---

## 🧠 Observation

Constraint:

```
1 ≤ value ≤ 1000
```

So instead of Map:

```
Use direct indexing
```

---

## 💡 Idea

```
freq[value] += weight
```

Then traverse array once.

---

## 💻 Code 

```java
class Solution {
    public List<List<Integer>> mergeSimilarItems(int[][] items1, int[][] items2) {
        int[] freqArray = new int[1001];
        for(int[] element : items1) {
            freqArray[element[0]] += element[1];
        }

        for(int[] element : items2) {
            freqArray[element[0]] += element[1];
        }

        List<List<Integer>> list = new ArrayList<>();
        for(int i = 1; i < 1001; i++) {
            if(freqArray[i] > 0) {
                list.add(new ArrayList<>(Arrays.asList(i, freqArray[i])));
            }
        }

        return list;
    }
}
```

---

## ⏱ Complexity

```
Time  : O(N + 1000)
≈ O(N)

Space : O(1000)
```

🔥 Fastest approach.

---

---

# 🧩 Comparison

| Approach | Sorting Needed | Speed |
|---|---|---|
| HashMap | ✅ Yes | Better |
| TreeMap | ❌ No | Good |
| Frequency Array | ❌ No | ⭐ Best |

---
| Structure | Insert   | Sorting        | Overall           |
| --------- | -------- | -------------- | ----------------- |
| HashMap   | O(1)     | sort once      | ✅ Faster          |
| TreeMap   | O(log n) | already sorted | ❌ Slightly slower |


---

# 🏆 Interview Insight

Whenever you see:

```
value range is SMALL
```

Think instantly:

```
Frequency Array instead of HashMap
```

---

# 🔥 Pattern Learned

```
Counting / Aggregation Pattern
```

Used in:

✅ Counting Sort  
✅ Frequency Problems  
✅ Bucket Problems  
✅ Histogram Logic  

---

