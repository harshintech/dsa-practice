# LeetCode 27 – Remove Element

## 🧠 Problem
Given an integer array `nums` and an integer `val`, remove all occurrences of `val` **in-place** and return the number of elements not equal to `val`.

The order of the elements may be changed.  
It is not necessary to consider elements beyond the returned length.

---

## 🧩 Pattern & Data Structure

- **Pattern:** Two Pointers (Read & Write)
- **Data Structure:** Array

---

## 💡 Approach (Two Pointer – Read & Write)

We use two pointers:

- `i` → **reader pointer** to scan the array
- `k` → **writer pointer** to place valid elements

Steps:
1. Traverse the array using pointer `i`
2. If `nums[i]` is not equal to `val`, copy it to `nums[k]`
3. Increment `k` after placing a valid element
4. After traversal, `k` represents the count of elements not equal to `val`

This approach modifies the array **in-place** without using extra space.

---

## 🧮 Complexity Analysis

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

---

## ✅ Java Implementation

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int k = 0;

        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != val) {
                nums[k] = nums[i];
                k++;
            }
        }

        return k;
    }
}
