# 🔢 Evaluate Reverse Polish Notation (RPN)

---

## 📌 Problem

Given tokens representing an expression in **Reverse Polish Notation (Postfix)**.

Example:

```
["2","1","+","3","*"]
```

Evaluate and return result.

---

## 🧠 What is Reverse Polish Notation?

Infix (normal math):

```
2 + 1
```

Postfix (RPN):

```
2 1 +
```

Operator comes **after operands**.

---

## ✅ Code (UNCHANGED)

```java
class Solution {
    public int evalRPN(String[] tokens) {

        Stack<Integer> stack = new Stack<>();

    
        for(String c: tokens){

            if(c.equals("+")){
                stack.push(stack.pop() + stack.pop());
            }else if(c.equals("-")){
                int second = stack.pop();
                int first = stack.pop();
                stack.push(first - second);
            }else if(c.equals("*")){
                stack.push(stack.pop() * stack.pop());
            }else if(c.equals("/")){
                 int second = stack.pop();
                int first = stack.pop();
                stack.push(first / second);
            }else{
                stack.push(Integer.parseInt(c));
            }
        }
        return stack.peek();
    }
}
```

---

# 🎯 Core Idea

Use a stack.

Algorithm:

```
1. If number → push to stack
2. If operator → pop two numbers
3. Apply operation
4. Push result back
```

---

# 🔥 VERY IMPORTANT PART

### Order Matters for `-` and `/`

When operator comes:

```
second = stack.pop()
first  = stack.pop()
```

Then:

```
first - second
first / second
```

NOT:

```
second - first ❌
```

Because stack is LIFO.

---

# 🧩 Example 1

Input:

```
["2","1","+","3","*"]
```

Step-by-step:

Push 2  
Push 1  

Encounter `+`

```
1 + 2 = 3
```

Push 3  

Push 3  

Encounter `*`

```
3 * 3 = 9
```

Answer:

```
9
```

---

# 🧩 Example 2 (Order Important)

Input:

```
["4","13","5","/","+"]
```

Process:

Push 4  
Push 13  
Push 5  

Encounter `/`

```
first = 13
second = 5
13 / 5 = 2
```

Push 2  

Encounter `+`

```
4 + 2 = 6
```

Answer:

```
6
```

---

# 🚀 Why Stack Works Perfectly

Postfix naturally follows:

```
Operands first
Operator later
```

So when operator appears:

Operands are already in stack.

---

# ⏱ Complexity

### Time
```
O(n)
```

One pass.

### Space
```
O(n)
```

Worst case all numbers.

---

# 🏆 Pattern Recognition

If problem contains:

```
Postfix
Prefix
Expression evaluation
```

Think:

```
STACK
```

---

# 🔥 Common Interview Trap

Many people write:

```java
stack.push(stack.pop() - stack.pop());
```

This is WRONG.

Because order reverses.

Always:

```
second = pop()
first = pop()
first - second
```

---

# 🧠 Golden Memory Rule

```
Operator sees stack like:
[ first , second ]

But pop order is:
second first
```

So assign carefully.

---

# 🚀 Advanced Insight

This is foundation for:

✅ Expression parsing  
✅ Compiler design  
✅ Infix → Postfix conversion  
✅ Calculator problems  

---
