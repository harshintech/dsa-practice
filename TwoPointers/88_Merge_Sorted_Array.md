# LeetCode 88 - Merge Sorted Array 

## 🧠 Problem Statement
You are given two sorted integer arrays `nums1` and `nums2`, and two integers `m` and `n` representing the number of valid elements in each array.

- `nums1` has a length of `m + n`, where the last `n` elements are empty (`0`) and should be filled.
- `nums2` has a length of `n`.

Your task is to **merge `nums2` into `nums1` as one sorted array**, modifying `nums1` in-place.

---

## 💡 Approach (Two Pointer – From Back)

To avoid overwriting elements in `nums1`, we merge the arrays **from the end**.

### Pointers Used:
- `i` → last valid element in `nums1` (`m - 1`)
- `j` → last element in `nums2` (`n - 1`)
- `k` → last index of `nums1` (`m + n - 1`)

### Steps:
1. Compare `nums1[i]` and `nums2[j]`
2. Place the larger value at `nums1[k]`
3. Move the pointers accordingly
4. After the loop, copy remaining elements of `nums2` (if any)

---

## ✅ Java Solution

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {

        int k = nums1.length - 1;
        int i = m - 1;
        int j = n - 1;

        while (i >= 0 && j >= 0) {
            if (nums1[i] < nums2[j]) {
                nums1[k] = nums2[j];
                j--;
            } else {
                nums1[k] = nums1[i];
                i--;
            }
            k--;
        }

        // Copy remaining elements of nums2 (if any)
        while (j >= 0) {
            nums1[k] = nums2[j];
            j--;
            k--;
        }
    }
}
```
