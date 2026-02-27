# 🧱 MinStack (All Operations in O(1))

---

## 📌 Problem

Design a stack that supports:

```
push()
pop()
top()
getMin()
```

⚡ All operations must run in **O(1)** time.

---

## ✅ Code

```java
class MinStack {

    private List<int[]> st;

    public MinStack() {
         st = new ArrayList<>();
    }
    
    public void push(int val) {
        int[] top = st.isEmpty() ? new int[]{val,val} : st.get(st.size() - 1);
        int min_val = top[1];
        if(min_val > val){
            min_val = val;
        } 
        
        st.add(new int[]{val,min_val});
    }
    
    public void pop() {
        st.remove(st.size() - 1);
    }
    
    public int top() {
        return st.isEmpty() ? -1 : st.get(st.size()-1)[0];
    }
    
    public int getMin() {   
        return st.isEmpty() ? -1 : st.get(st.size() -1)[1];
    }
}
```

---

# 🧠 Core Idea

Instead of storing only:

```
[value]
```

We store:

```
[value, currentMinimumTillNow]
```

So every element remembers:

```
What was the minimum when I was pushed?
```

---

# 🎯 Why This Works

When pushing a value:

```
newMin = min(currentValue, previousMin)
```

So each element stores:

```
[val, minSoFar]
```

This way:

```
getMin() → just look at top element's min
```

No traversal needed.

---

# 🔥 Example Flow

### Push 5

Stack:

```
[5,5]
```

Min = 5

---

### Push 3

Previous min = 5  
New min = min(3,5) = 3  

Stack:

```
[5,5]
[3,3]
```

Min = 3

---

### Push 7

Previous min = 3  
New min = min(7,3) = 3  

Stack:

```
[5,5]
[3,3]
[7,3]
```

Min still = 3

---

### Pop

Remove:

```
[7,3]
```

Top becomes:

```
[3,3]
```

Min automatically restored = 3 ✅

---

# 🧩 Why No Extra Work Needed

Because:

Every node already stored its minimum at that time.

So when popping:

We automatically return to previous minimum.

No recalculation required.

---

# ⏱ Complexity

### push()
```
O(1)
```

### pop()
```
O(1)
```

### top()
```
O(1)
```

### getMin()
```
O(1)
```

---

# 💾 Space Complexity

```
O(n)
```

We store 2 values per element.

---

# 🏆 Interview Pattern

This is a classic:

```
Store extra information inside stack
```

Instead of using:

```
Second stack for minimum
```

Both approaches are valid.

---

# 🔥 Alternative Approach (Concept Only)

You can also maintain:

```
mainStack
minStack
```

Push into minStack only when new minimum found.

But your solution is cleaner.

---

# 🧠 Golden Concept

```
Augmented Stack
```

Meaning:

We enhance each element with extra info to maintain O(1).

---

# 🚀 Pattern Recognition

Used in:

✅ Max Stack  
✅ Design problems  
✅ Sliding window minimum  
✅ Monotonic stack variations  

---

