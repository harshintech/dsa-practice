# LeetCode 621 - Task Scheduler (Least Interval)

---

## 📌 Problem

You are given:

- `tasks[]` → array of capital letters (A–Z)
- `n` → cooling interval

After executing a task, the same task must wait `n` units of time before being executed again.

Return the **minimum time units** required to finish all tasks.

---

## 🧩 Example

Input:
```
tasks = ["A","A","A","B","B","B"]
n = 2
```

Output:
```
8
```

Possible schedule:
```
A → B → idle → A → B → idle → A → B
```

---

# 🚀 Approach (Max Heap + Cooling Queue)

---

## 🔑 Key Idea

We always want to execute:

```
Task with highest remaining frequency
```

So we use:

### 1️⃣ Max Heap → to pick most frequent task  
### 2️⃣ Queue → to handle cooling period  

---

# 💻 Your Java Code

```java
class Solution {

    class Task implements Comparable<Task>{
        int freq = 0;
        int executionTime = 0;

        public Task(int freq,int executionTime){
            this.freq = freq;
            this.executionTime = executionTime;
        }

        public int compareTo(Task task){
            return task.freq - this.freq;   // max heap by freq
        }
    }

    public int leastInterval(char[] tasks, int n) {
        
        HashMap<Character,Integer> freqMap = new HashMap<>();
        for(Character ch: tasks){
            freqMap.put(ch,freqMap.getOrDefault(ch,0)+1);
        }

        PriorityQueue<Task> pq = new PriorityQueue<>();
        for(Character ch: freqMap.keySet()){
            pq.offer(new Task(freqMap.get(ch),0));
        }

        Queue<Task> queue = new LinkedList<>();

        int time = 0;

        while(!queue.isEmpty() || !pq.isEmpty()){
            time++;

            // Execute highest frequency task
            if(!pq.isEmpty()){
                Task task = pq.poll();
                task.freq--;

                if(task.freq > 0){
                    task.executionTime = time + n;
                    queue.offer(task);
                }
            }

            // Check if cooling completed
            if(!queue.isEmpty() && queue.peek().executionTime == time){
                pq.offer(queue.poll());
            }
        }

        return time;
    }
}
```

---

# 🎯 How It Works

At each time unit:

1. Increase time
2. Execute most frequent available task
3. Put it in cooling queue
4. When cooling time finishes → push back to heap

Loop continues until:

```
pq empty AND queue empty
```

---

# 🎨 Dry Run Example

```
tasks = [A,A,A,B,B,B]
n = 2
```

Frequency:
```
A = 3
B = 3
```

Time simulation:

```
1 → A
2 → B
3 → idle
4 → A
5 → B
6 → idle
7 → A
8 → B
```

Total:
```
8
```

---

# ⏱ Time Complexity

Let:

```
T = total tasks
```

Each task processed once.

```
O(T log 26)
```

Since max 26 characters.

Effectively:
```
O(T)
```

---

# 📦 Space Complexity

```
O(26)
```

Because at most 26 different tasks.

---

# 🔥 Pattern Used

Greedy  
Max Heap  
Queue for Cooling  
Time Simulation  

---

# 🏆 Interview Insight

This is combination of:

- Top K pattern
- Simulation
- Scheduling problem
- Greedy strategy

Very common FAANG question.

---

# ⚠ Important Concept

We simulate time instead of calculating formula.

Alternative formula approach exists:

```
(maxFreq - 1) * (n + 1) + countOfMaxFreq
```

Then take:

```
max(totalTasks, formula)
```

But your solution is more intuitive and safe.

---

# ✅ Final Output

Input:
```
["A","A","A","B","B","B"], n=2
```

Output:
```
8
```

---

# 🧠 Final Verdict On Your Code

✔ Correct logic  
✔ Good heap usage  
✔ Proper cooling handling  
✔ Clean class structure  

This is strong implementation.

