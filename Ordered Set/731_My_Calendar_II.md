# 📅 MyCalendar II — No Triple Booking 
### Used Sweep Line ( ⭐ Most Important ) 

---

## 📌 Problem

Design a calendar system where:

✅ Double booking allowed  
❌ Triple booking NOT allowed  

Meaning:

```
At any time,
active events ≤ 2
```

---

## 🧠 Core Idea — Sweep Line Algorithm

Instead of storing intervals directly:

We store **timeline changes**.

---

## 🔥 Trick Used

For every booking:

```
+1 at startTime
-1 at endTime
```

Then calculate:

```
Prefix Sum → Active meetings
```

---

## 💻 Code

```java
class MyCalendarTwo {

    private TreeMap<Integer, Integer> calendar;

    public MyCalendarTwo() {
        calendar = new TreeMap<>();
    }
    
    public boolean book(int startTime, int endTime) {

        calendar.put(startTime, calendar.getOrDefault(startTime, 0) + 1);
        calendar.put(endTime, calendar.getOrDefault(endTime, 0) - 1);

        int active = 0;

        for (int count : calendar.values()) {
            active += count;
            if (active > 2) {
                // rollback
                calendar.put(startTime, calendar.get(startTime) - 1);
                calendar.put(endTime, calendar.get(endTime) + 1);

                if (calendar.get(startTime) == 0)
                    calendar.remove(startTime);

                if (calendar.get(endTime) == 0)
                    calendar.remove(endTime);

                return false;
            }
        }

        return true;
    }
}
```

---

# 🌊 Sweep Line Visualization

Think timeline like this:

```
Time →
```

Each booking adds:

```
start → +1
end   → -1
```

---

# ✅ Step-by-Step Dry Run

---

## ✅ book(10,20)

Map:

```
10 → +1
20 → -1
```

Prefix Sum:

```
10 → active = 1
20 → active = 0
```

✅ Allowed

---

## ✅ book(50,60)

```
50 → +1
60 → -1
```

Active never exceeds 1.

✅ Allowed

---

## ✅ book(10,40)

Update:

```
10 → +2
40 → -1
```

Timeline:

```
10 → active = 2
```

Double booking allowed ✅

---

## ❌ book(5,15)

Add:

```
5  → +1
15 → -1
```

Prefix:

```
5  → 1
10 → 3 ❌
```

Triple booking detected.

---

## 🔁 Rollback Happens

We undo:

```
startTime change
endTime change
```

Calendar restored.

Return:

```
false
```

---

## ✅ book(5,10)

Active count:

```
max = 2
```

Allowed ✅

---

## ✅ book(25,55)

Active count remains ≤ 2.

Allowed ✅

---

# 🧩 Why TreeMap?

TreeMap keeps times sorted automatically:

```
timeline processed chronologically
```

Needed for prefix sum simulation.

---

# ⚡ Key Insight

```
We DO NOT store intervals.
We store event changes.
```

This converts interval overlap problem into:

```
Running sum problem
```

---

# 🔥 Sweep Line Concept

Used in:

✅ Calendar problems  
✅ Meeting rooms  
✅ Skyline problem  
✅ Maximum overlaps  
✅ Interval counting  

---

# ⏱ Complexity

### Booking
```
O(N)
```

(prefix traversal)

---

### Space
```
O(N)
```

stored timeline points.

---

# 🏆 Golden Interview Insight

```
Interval overlap
→ convert into timeline changes
→ apply prefix sum
```

This is called:

```
Sweep Line Algorithm
```

---

# 🚀 Difference from MyCalendar I

| Problem | Allowed |
|---|---|
| MyCalendar I | No overlap |
| MyCalendar II | Double allowed |
| MyCalendar III | Count maximum overlap |

---

# 🔥 Mental Model

```
Start → people enter room
End   → people leave room
```

Never allow:

```
people inside > 2
```

---

