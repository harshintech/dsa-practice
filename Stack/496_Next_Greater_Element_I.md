# LeetCode 496 - Next Greater Element I

---

## 📌 Problem

You are given two arrays:

- `nums1`
- `nums2`

All elements of `nums1` are present in `nums2`.

For each element in `nums1`, find the **next greater element** in `nums2`.

The next greater element of a number `x` is the first greater number to its right in `nums2`.  
If it does not exist, return `-1`.

---

## 🧩 Example

Input:
```
nums1 = [4,1,2]
nums2 = [1,3,4,2]
```

Output:
```
[-1,3,-1]
```

Explanation:

- 4 → no greater element → -1  
- 1 → next greater is 3  
- 2 → no greater element → -1  

---

# 🚀 Approach (Monotonic Stack + HashMap)

## 🔑 Key Idea

We solve this in two steps:

### Step 1 → Precompute Next Greater for nums2

- Traverse `nums2` from right to left.
- Use a **monotonic decreasing stack**.
- For each element:
  - Pop smaller elements.
  - Top of stack = next greater element.
  - Store in HashMap.

### Step 2 → Build Answer for nums1

- For each element in `nums1`
- Directly fetch result from HashMap.

---

# 💻 Java Code

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        
        HashMap<Integer,Integer> map = new HashMap<>();
        Stack<Integer> st = new Stack<>();

        for(int i = nums2.length - 1; i >= 0; i--){

            int currVal = nums2[i];

            while(!st.isEmpty() && st.peek() <= currVal){
                st.pop();
            }

            if(st.isEmpty()){
                map.put(currVal, -1);
            } else {
                map.put(currVal, st.peek());
            }
            
            st.push(currVal);
        }

        int ans[] = new int[nums1.length];

        for(int i = 0; i < nums1.length; i++){
            ans[i] = map.get(nums1[i]);
        }

        return ans;
    }
}
```

---

# 🎨 Graphical Representation

Example:

```
nums2 = [1,3,4,2]
```

Traverse from right → left

---

### Step 1

Start from 2:

Stack: []
Next Greater of 2 → -1

Stack:
```
[2]
```

---

### Step 2

Element = 4

Pop 2 (since 2 ≤ 4)

Stack empty → Next Greater = -1

Stack:
```
[4]
```

---

### Step 3

Element = 3

Top = 4 (greater)

Next Greater of 3 → 4

Stack:
```
[4,3]
```

---

### Step 4

Element = 1

Top = 3 (greater)

Next Greater of 1 → 3

Stack:
```
[4,3,1]
```

---

Final Map:

```
1 → 3
3 → 4
4 → -1
2 → -1
```

---

Now build answer for:

```
nums1 = [4,1,2]
```

Result:

```
[-1,3,-1]
```

---

# ⏱ Time Complexity

O(n + m)

- Each element pushed once.
- Each element popped once.
- Building answer is linear.

---

# 📦 Space Complexity

O(n)

- Stack
- HashMap

---

# 🧠 Why This Works

Monotonic stack ensures:

- We always keep only useful candidates.
- We efficiently find the next greater element in one pass.

Without stack → brute force would be O(n²).

---

# 🔥 Pattern Used

Monotonic Stack  
Next Greater Element  
Stack + HashMap  

---

# ⚡ Interview Insight

If interviewer asks:

Why traverse from right to left?

Because we want to know the **next greater element on the right**.  
Traversing backward makes it easy to maintain the stack.

---

# ✅ Final Output

Input:
```
nums1 = [4,1,2]
nums2 = [1,3,4,2]
```

Output:
```
[-1,3,-1]
```

