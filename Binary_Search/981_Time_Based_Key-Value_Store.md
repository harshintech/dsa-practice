# ⏳ Time Based Key-Value Store (TimeMap)

---

## 📌 Problem

Design a data structure that supports:

```
set(key, value, timestamp)
get(key, timestamp)
```

### Rules

✅ Store multiple values for same key  
✅ Each value has timestamp  
✅ get() should return:

```
value having largest timestamp ≤ given timestamp
```

If not found → return `""`

---

# ✅ Code

```java
class Data {
    String val;
    int time;

    Data(String val, int time) {
        this.val = val;
        this.time = time;
    }
}

class TimeMap {

    Map<String, List<Data>> map;

    public TimeMap() {
        map = new HashMap<String, List<Data>>();
    }

    public void set(String key, String value, int timestamp) {
        map.computeIfAbsent(key, k -> new ArrayList<Data>()).add(new Data(value,timestamp));
    }

    public String get(String key, int timestamp) {
        if(!map.containsKey(key)) return "";
        return binarySearch(map.get(key),timestamp);
    }

    private String binarySearch(List<Data> list,int time){
        int left = 0,right = list.size()  - 1;
        while(left < right){
            int mid = (left + right + 1) / 2;

            if(time < list.get(mid).time){
                right = mid - 1;
            }else{
                left = mid;
            }
        }

        return list.get(left).time <= time ? list.get(left).val : "";
    }
}
```

---

# 🧠 Data Structure Used

```
HashMap<String, List<Data>>
```

Meaning:

```
key → list of (value, timestamp)
```

Example storage:

```
set("foo","bar",1)
set("foo","bar2",4)
```

Stored as:

```
foo → [(bar,1), (bar2,4)]
```

---

# 🔥 VERY IMPORTANT OBSERVATION

Problem guarantees:

```
timestamps are strictly increasing
```

So list becomes:

```
SORTED automatically ✅
```

That allows:

```
Binary Search
```

---

# ⚡ set() Operation

```java
map.computeIfAbsent(key,
        k -> new ArrayList<>())
        .add(new Data(value,timestamp));
```

### Meaning

If key not present:

```
create new list
```

Then add value.

Equivalent to:

```
if(!map.containsKey(key))
    create list
add data
```

---

# 🔍 get() Operation

Goal:

```
Find latest timestamp ≤ given time
```

Example:

Stored:

```
[(bar,1), (bar2,4)]
```

Query:

```
get("foo",3)
```

Expected:

```
bar
```

Because:

```
1 ≤ 3
4 > 3
```

---

# 🚀 Why Binary Search?

Linear search:

```
O(n)
```

Binary search:

```
O(log n)
```

Huge optimization.

---

# 🧩 Binary Search Logic

We want:

```
RIGHTMOST valid timestamp
```

Condition:

```
timestamp <= given time
```

---

## Important Line

```java
int mid = (left + right + 1) / 2;
```

### Why `+1` ?

Prevents infinite loop.

This forces search toward **right side**.

Called:

```
Upper Bound Binary Search
```

---

# 📊 Dry Run

List:

```
[(bar,1),(bar2,4),(bar3,6)]
```

Search:

```
timestamp = 5
```

---

### Step 1

```
left=0 right=2
mid=1
time=4 <=5
→ move left
```

```
left=1
```

---

### Step 2

```
left=1 right=2
mid=2
time=6 >5
→ move right
```

```
right=1
```

Now:

```
left == right
```

Answer index = 1 ✅

Return:

```
bar2
```

---

# ✅ Final Check

```java
list.get(left).time <= time
```

If valid → return value  
Else → return empty string

---

# ⏱ Complexity

## set()
```
O(1)
```

## get()
```
O(log n)
```

(Binary Search)

---

# 💾 Space Complexity

```
O(total number of sets)
```

---

# 🏆 Pattern Recognition

If problem contains:

```
Version history
Time snapshots
Closest smaller timestamp
```

Think:

```
HashMap + Binary Search
```

---

# 🔥 Interview Insight

This problem tests:

✅ Data modeling  
✅ Binary Search variation  
✅ Rightmost valid search  
✅ Optimized retrieval  

---

# 🧠 Golden Rule

```
Store history
Search latest valid version
```

---

You just implemented a **real database concept**:

```
Time Versioned Storage ✅
```

(Meta / Google level concept)

---

