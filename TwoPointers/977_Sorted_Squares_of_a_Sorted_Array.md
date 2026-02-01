# LeetCode 977 - Sorted Squares of a Sorted Array

---

## 📌 Problem

Given an integer array `nums` sorted in non-decreasing order,  
return an array of the squares of each number sorted in non-decreasing order.

---

## 🧩 Example

Input:
```
nums = [-4, -1, 0, 3, 10]
```

Output:
```
[0, 1, 9, 16, 100]
```

---

## 🚀 Approach (Two Pointer Technique)

### Key Observation

- The array is already sorted.
- But negative numbers become positive after squaring.
- The largest square will come from either:
  - Leftmost element
  - Rightmost element

So we use **two pointers**:

- `left` → start of array
- `right` → end of array
- Fill result array from **end to beginning**

---

## 💡 Algorithm Steps

1. Create result array of same size.
2. Compare absolute values of:
   - `nums[left]`
   - `nums[right]`
3. Put larger square at the end of result array.
4. Move the corresponding pointer.
5. Repeat until all positions filled.

---

## 💻 Java Code

```java
class Solution {
    public int[] sortedSquares(int[] nums) {

        int[] res = new int[nums.length];
        int left = 0;
        int right = nums.length - 1;

        for (int i = nums.length - 1; i >= 0; i--) {
            if (Math.abs(nums[left]) > Math.abs(nums[right])) {
                res[i] = nums[left] * nums[left];
                left++;
            } else {
                res[i] = nums[right] * nums[right];
                right--;
            }
        }
        return res;
    }
}
```

---

## 🎨 Graphical Representation

Example:
```
nums = [-4, -1, 0, 3, 10]
```

Initial:

```
-4  -1   0   3   10
 ↑                   ↑
left                right
```

Compare | -4 | = 4  
Compare | 10 | = 10  

10 is bigger → put 100 at end.

```
res = [_, _, _, _, 100]
```

Move right pointer.

---

Now:

```
-4  -1   0   3   10
 ↑               ↑
left            right
```

Compare | -4 | = 4  
Compare | 3 | = 3  

4 is bigger → put 16

```
res = [_, _, _, 16, 100]
```

Move left pointer.

---

Continue:

```
-4  -1   0   3   10
     ↑           ↑
```

Compare | -1 | = 1  
Compare | 3 | = 3  

Put 9

```
res = [_, _, 9, 16, 100]
```

---

Final result:

```
[0, 1, 9, 16, 100]
```

---

## ⏱ Time Complexity

O(n)

- Single pass through array.

---

## 📦 Space Complexity

O(n)

- Extra result array used.

---

## 🧠 Why This Works

- Largest square always comes from either extreme.
- Filling from back ensures sorted order.
- Two pointers make it linear time.

---

## ✅ Final Answer

Input:
```
[-4, -1, 0, 3, 10]
```

Output:
```
[0, 1, 9, 16, 100]
```

---

## 🔥 Pattern Used

Two Pointers  
Array Traversal  
Greedy Placement





