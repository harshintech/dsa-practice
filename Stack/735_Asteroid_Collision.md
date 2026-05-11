# ☄️ Asteroid Collision

---

## 📌 Problem

Each asteroid is represented by an integer:

- Positive (`+`) → moving right
- Negative (`-`) → moving left
- Absolute value = size

When two asteroids collide:

- Smaller one explodes
- If equal sizes, both explode
- Asteroids moving in the same direction never collide

Return the final state after all collisions.

---

## ✅ Code (UNCHANGED)

```java
class Solution {
    public int[] asteroidCollision(int[] asteroids) {
        Stack<Integer> st = new Stack<>();
        for(int a : asteroids){

            //when collision happens ??
            while(!st.isEmpty() && a < 0 && st.peek() > 0){
                int sum = a + st.peek();

                if(sum < 0){
                    st.pop();
                }else if(sum > 0){
                    a = 0;
                }else{ //sum == 0
                    st.pop(); 
                    a = 0;
                }
            }

            if(a != 0){
                st.push(a);
            }
        }

        int s = st.size();
        int[] result = new int[s];
        int i = s-1;
        while(!st.isEmpty()){
            result[i] = st.peek();
            st.pop();
            i--;
        }

        return result;
    }
}
```

---

# 🧠 Core Idea

We process asteroids from left to right.

The stack stores asteroids that have survived so far.

For every new asteroid:

1. Check whether it collides with the stack top.
2. Resolve the collision.
3. Push it if it survives.

---

# 💥 When Does Collision Happen?

Collision is possible only when:

```java
a < 0 && st.peek() > 0
```

Meaning:

- Stack top is moving right (`+`)
- Current asteroid is moving left (`-`)

They are moving toward each other.

---

## Visual

```text
+5   -3
 →   ←
```

These will collide.

---

# 🚫 Cases Where Collision Does NOT Happen

```text
-5  -3   (both left)
+5  +3   (both right)
-5  +3   (moving away)
```

---

# 🧮 Why `sum = a + st.peek()` Works

Suppose:

```text
a = -8
top = +5
```

```text
sum = -8 + 5 = -3
```

Negative result means current asteroid is larger.

---

## Interpretation

### `sum < 0`

```text
|a| > |top|
```

Current asteroid survives.

Pop stack top and continue checking.

---

### `sum > 0`

```text
|top| > |a|
```

Current asteroid explodes.

Set:

```java
a = 0;
```

---

### `sum == 0`

Equal sizes.

Both explode.

- Pop stack top
- Set `a = 0`

---

# 🔄 Why `while` Instead of `if`?

A large asteroid may destroy multiple previous asteroids.

Example:

```text
[10, 2, -5]
```

Process `-5`:

1. Collides with `2` → `2` explodes
2. Then collides with `10`

So repeated checking is required.

---

# 📊 Dry Run

Input:

```text
[5, 10, -5]
```

---

## Step 1

Push `5`

```text
stack = [5]
```

---

## Step 2

Push `10`

```text
stack = [5, 10]
```

---

## Step 3

Current `a = -5`

Collision with `10`

```text
-5 + 10 = 5 > 0
```

`10` survives, `-5` explodes.

```text
stack = [5, 10]
```

---

## Final Output

```text
[5, 10]
```

---

# 📊 Another Example

Input:

```text
[8, -8]
```

Collision:

```text
-8 + 8 = 0
```

Both explode.

Output:

```text
[]
```

---

# 🏗 Building Result Array

Stack stores elements from left to right, but popping gives them in reverse order.

So we fill the array from the end:

```java
int i = s - 1;
```

---

# ⏱ Complexity

### Time

```text
O(n)
```

Each asteroid is pushed and popped at most once.

### Space

```text
O(n)
```

For the stack.

---

# 🏆 Pattern Recognition

If problem involves:

- Collisions
- Elimination
- Comparing with recent survivors

Think:

```text
Stack
```

---
