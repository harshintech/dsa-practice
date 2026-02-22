# 📅 MyCalendar I (TreeMap Interval Booking)

---

## 📌 Problem

Design a calendar system that allows booking events:

```
[startTime, endTime)
```

Rules:

✅ Events must NOT overlap  
✅ Return `true` if booking possible  
❌ Return `false` if conflict occurs  

---

## 🧠 Core Idea

We must check:

```
Does new interval overlap
with existing intervals?
```

Instead of checking ALL bookings ❌

We use:

```
TreeMap (Sorted Map)
```

---

# 🌳 Why TreeMap?

TreeMap automatically keeps keys sorted.

We store:

```
startTime → endTime
```

Example:

```
calendar =
{
 10 → 20
 25 → 30
}
```

So events are ordered by start time.

---

# 💻 Code 

```java
class MyCalendar {

    private TreeMap<Integer, Integer> calendar;

    public MyCalendar() {
        calendar = new TreeMap<>();
    }
    
    public boolean book(int startTime, int endTime) {
        
        //Integer store null value int not store null value
        // [1,2,3,4,5,6]
        // floorKey(4) = 3
        // ceilingKey(4) = 5
        Integer prev = calendar.floorKey(startTime);
        if(prev != null && calendar.get(prev) > startTime){
            return false;
        }

        Integer next = calendar.ceilingKey(startTime);
        if (next != null && next < endTime) {
            return false; // overlap
        }

        calendar.put(startTime, endTime);
        return true;
    }
}
```

---

# 🔥 Important TreeMap Functions

---

## 🌳 1️⃣ floorKey(key)

### Definition

```
Greatest key ≤ given key
```

👉 Closest element on LEFT side.

---

### Example

Keys:

```
10   20   30
```

```
floorKey(25) → 20
floorKey(20) → 20
floorKey(5)  → null
```

---

## 🌳 2️⃣ ceilingKey(key)

### Definition

```
Smallest key ≥ given key
```

👉 Closest element on RIGHT side.

---

### Example

```
ceilingKey(25) → 30
ceilingKey(20) → 20
ceilingKey(35) → null
```

---

# 🧠 Visual Understanding

Existing bookings:

```
10 ----- 20
        25 ----- 30
```

New booking:

```
startTime = 22
```

```
floorKey(22)   → 10
ceilingKey(22) → 25
```

Only neighbors can overlap ✅

---

# 🚨 Overlap Conditions

---

## ✅ Check Previous Event

```
prevEnd > startTime
```

Meaning:

```
Previous meeting still running
```

Example:

```
Existing : [10,20)
New      :     [15,25)
```

❌ Conflict

---

## ✅ Check Next Event

```
nextStart < endTime
```

Example:

```
Existing :       [25,30)
New      : [20,28)
```

❌ Conflict

---

# ✅ Safe Booking

If both checks pass:

```
No overlap exists
```

Insert event.

---

# ⏱ Complexity

### Booking Time
```
O(log N)
```

(TreeMap search)

---

### Space
```
O(N)
```

Stored events.

---

# 🔥 Why Only Neighbours?

Because TreeMap keeps intervals sorted:

```
Only adjacent intervals
can overlap.
```

No need to scan whole calendar 🚀

---

# 🎯 Memory Trick

```
floor   → LEFT neighbour
ceiling → RIGHT neighbour
```

---

# 🏆 Interview Insight

This problem teaches:

```
Ordered Map + Interval Conflict Checking
```

Used in:

✅ Meeting Rooms  
✅ Interval Scheduling  
✅ Timeline Systems  
✅ Booking Engines  

---

# 🚀 Advanced Follow-ups

Next problems:

✅ MyCalendar II  
✅ MyCalendar III  
✅ Range Module  
✅ Interval Tree Design  

---
