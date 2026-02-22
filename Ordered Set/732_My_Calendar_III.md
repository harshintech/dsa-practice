# 📅 MyCalendar III — Maximum Overlapping Events

---

## 📌 Problem

Design a calendar system.

Each booking:

```
[startTime, endTime)
```

After every booking return:

```
Maximum number of overlapping events so far.
```

This value is called:

```
K-booking
```

---

## 🎯 Meaning

If at some time:

```
3 events overlap
```

Return:

```
3
```

---

## 🧠 Core Idea — Sweep Line Algorithm

Same idea as **MyCalendar II**, but now:

```
We DO NOT reject booking.
```

Instead:

```
Track maximum simultaneous events.
```

---

# 🔥 Timeline Trick

For every booking:

```
start → +1
end   → -1
```

Then compute:

```
Prefix Sum
```

which gives:

```
active events at each time
```

---

# 💻 Code 

```java
class MyCalendarThree {

    private TreeMap<Integer, Integer> calendar;

    public MyCalendarThree() {
          calendar = new TreeMap<>();
    }
    
    public int book(int startTime, int endTime) {
        calendar.put(startTime, calendar.getOrDefault(startTime, 0) + 1);
        calendar.put(endTime, calendar.getOrDefault(endTime, 0) - 1);

        int active = 0;
        int maxActive = Integer.MIN_VALUE;

         for (int count : calendar.values()) {
            active += count;
            maxActive = Math.max(active,maxActive);
        }

        return maxActive;
    }
}
```

---

# 🌊 Sweep Line Visualization

Bookings:

```
book(10,20)
book(15,25)
book(17,30)
```

---

## Timeline Changes

```
10 → +1
15 → +1
17 → +1
20 → -1
25 → -1
30 → -1
```

---

## Prefix Sum Calculation

| Time | Change | Active |
|------|--------|--------|
|10|+1|1|
|15|+1|2|
|17|+1|3 ✅|
|20|-1|2|
|25|-1|1|
|30|-1|0|

---

✅ Maximum overlap:

```
3
```

Return:

```
3
```
Bookings:

```
[10,20], [15,25], [17,30]
```

---

# 🟢 Timeline with +1 / -1

```
Time → 10    15    17    20    25    30
        |     |     |     |     |     |

Event 1:  10 ---------------- 20   (+1 at 10, -1 at 20)
Event 2:        15 ---------------- 25   (+1 at 15, -1 at 25)
Event 3:              17 ---------------- 30   (+1 at 17, -1 at 30)
```

---

# 🟢 Line Sweep + Active Count

We will show **+1 / -1 on timeline** and **active count at that point**:

```
Time → 10    15    17    20    25    30
        |     |     |     |     |     |
Change: +1    +1    +1    -1    -1    -1
Active:  1     2     3     2     1     0
```

✅ Maximum active = 3

---

# 🟢 Graphical “Line + Event” view

```
Active Meetings
3 |              ________
2 |      _______|        |______
1 |  ____|                  |____
0 |_________________________________
    10    15     17    20    25    30
+1s ↑      ↑      ↑
-1s                         ↑      ↑      ↑
```

Legend:

* `↑` shows where a meeting starts (+1) or ends (-1)
* Horizontal line shows the duration of meeting
---

# 🧩 Why TreeMap?

TreeMap keeps keys:

```
Automatically sorted by time
```

Needed because prefix sum must follow timeline order.

---

# 🔥 Key Difference

---

## MyCalendar I

```
No overlap allowed
```

---

## MyCalendar II

```
Double allowed
Triple rejected
```

---

## MyCalendar III

```
Unlimited booking
Return maximum overlap
```

---

# ⚡ Mental Model

Imagine:

```
People entering and leaving room
```

```
start → person enters
end   → person leaves
```

We track:

```
Maximum people inside simultaneously
```

---

# ⏱ Complexity

### Per Booking
```
O(N)
```

(prefix traversal)

---

### Space
```
O(N)
```

timeline points stored.

---

# 🏆 Golden Interview Insight

```
Interval overlap problems
⇢ convert into timeline events
⇢ apply prefix sum
```

This technique is called:

# ⭐ Sweep Line Algorithm

---

# 🔥 Pattern Recognition

If problem mentions:

✅ overlapping intervals  
✅ concurrent events  
✅ meeting rooms  
✅ maximum active sessions  

👉 Think instantly:

```
Sweep Line
```

---

# 🚀 Interview Upgrade Insight

This problem is equivalent to:

```
Find maximum overlap among intervals
```

Same logic used in:

✅ Meeting Rooms II  
✅ Airplane traffic  
✅ CPU scheduling  
✅ Timeline analytics  

---

