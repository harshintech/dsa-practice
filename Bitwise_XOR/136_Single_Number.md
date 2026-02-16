# 🔢 Single Number (Using XOR)

---

## 📌 Problem

Given a non-empty array of integers:

- Every element appears **twice**
- Except for **one element**

Find that single element.

---

## 🧩 Example

Input:
```
[2, 1, 2, 3, 1]
```

Output:
```
3
```

---

# 🧠 XOR Properties (Very Important)

Let’s understand why XOR works.

---

## 🔑 XOR Rules

### 1️⃣ a ^ a = 0  
Same numbers cancel out.

```
5 ^ 5 = 0
```

---

### 2️⃣ a ^ 0 = a  

```
7 ^ 0 = 7
```

---

### 3️⃣ Commutative Property

```
a ^ b = b ^ a
```

Example:

```
5 ^ 3
101
011
----
110 = 6

3 ^ 5
011
101
----
110 = 6
```

---

### 4️⃣ Associative Property

```
(a ^ b) ^ c = a ^ (b ^ c)
```

We can rearrange order freely.

---

# 🚀 Why XOR Solves This Problem

Given:

```
[2, 1, 2, 3, 1]
```

Start:

```
res = 0
```

Process:

```
0 ^ 2 = 2
2 ^ 1 = 3
3 ^ 2 = 1
1 ^ 3 = 2
2 ^ 1 = 3
```

Final:

```
3
```

---

# 🧠 Mathematical Explanation

Rearranging:

```
0 ^ 2 ^ 1 ^ 2 ^ 3 ^ 1
```

Using commutative & associative:

```
0 ^ (2 ^ 2) ^ (1 ^ 1) ^ 3
```

Same numbers cancel:

```
0 ^ 0 ^ 0 ^ 3
```

Result:

```
3
```

---

# 💻 Java Code (Optimal)

```java
class Solution {
    public int singleNumber(int[] nums){

        int res = 0;

        for(int n : nums){
            res = res ^ n;
        }

        return res;
    }
}
```

---

# ⏱ Time Complexity

```
O(n)
```

One loop.

---

# 📦 Space Complexity

```
O(1)
```

No extra space.

---

# 🔥 Why This Is Powerful

- No sorting
- No extra map
- No nested loop
- Constant memory

---

# ❌ Brute Force Approach (Not Recommended)

```java
class Solution {
    public int singleNumber(int[] nums) {

        if(nums.length == 1)
            return nums[0];
 
        for(int i = 0; i < nums.length; i++){

            int count = 0;
            int x = nums[i];

            for(int j = 0; j < nums.length; j++){
                if(x == nums[j]){
                    count++;
                }
            }

            if(count == 1){
                return x;
            }
        }

        return -1;
    }
}
```

---

## ⏱ Brute Force Complexity

```
O(n²)
```

Very slow.

---

# 🏆 Pattern Used

Bit Manipulation  
XOR Cancellation  
Mathematical Properties  

---

# ⚡ Interview Insight

Whenever problem says:

- Every number appears twice
- Except one

Think:

```
XOR
```

---

# ✅ Final Answer

Input:
```
[2,1,2,3,1]
```

Output:
```
3
```

---


