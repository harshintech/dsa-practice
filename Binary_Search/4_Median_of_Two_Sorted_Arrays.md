# 🔥 Median of Two Sorted Arrays (Binary Search Partition Method)

---
## ( Note 📍) Read This if you take tress for this question
![image.png](https://assets.leetcode.com/users/images/726c060a-dd43-4cf2-8871-135be7c00eff_1771941067.9328272.png)

![image.png](https://assets.leetcode.com/users/images/2f5ce1f2-3469-43f3-9e13-02b10192c38d_1771941205.6600695.png)


## 🧠 Problem

Given:

```
nums1 (size = n1)
nums2 (size = n2)
```

Both sorted.

Find median in:

```
O(log(min(n1, n2)))
```

---

# 🚀 Core Idea

We do **Binary Search on smaller array**.

We try to:

```
Divide both arrays into LEFT half and RIGHT half
```

Such that:

```
Total elements in left = Total elements in right (almost equal)
```

---

# 📌 Code 

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {

        int n1 = nums1.length;
        int n2 = nums2.length;

        if (n1 > n2) {
            return findMedianSortedArrays(nums2, nums1);
        }

        int low = 0, high = n1;

        while (low <= high) {

            int cut1 = (low + high) / 2;
            int cut2 = (n1 + n2 + 1) / 2 - cut1;

            int l1 = (cut1 == 0) ? Integer.MIN_VALUE : nums1[cut1 - 1];
            int l2 = (cut2 == 0) ? Integer.MIN_VALUE : nums2[cut2 - 1];

            int r1 = (cut1 == n1) ? Integer.MAX_VALUE : nums1[cut1];
            int r2 = (cut2 == n2) ? Integer.MAX_VALUE : nums2[cut2];

             if (l1 <= r2 && l2 <= r1) {

                if ((n1+n2)%2==0)
                    return (Math.max(l1,l2)+Math.min(r1,r2))/2.0;
                else
                    return Math.max(l1,l2);
            }else if (l1 > r2)
                high = cut1 - 1;
            else
                low = cut1 + 1;
        }

        return 0;
    }
}
```

---

# 🎯 What is `cut1` and `cut2`?

They represent how many elements we take on LEFT side.

```
nums1:  [ 1  3 | 8  9  15 ]
               ↑ cut1

nums2:  [ 7 11 18 19 | 21 25 ]
                         ↑ cut2
```

---

# 🔥 Important Formula

```
cut2 = (n1 + n2 + 1) / 2 - cut1
```

Why?

Because:

```
Left half must contain (n1+n2+1)/2 elements
```

(+1 handles odd case automatically)

---

# 📌 What are l1, l2, r1, r2?

They represent boundary elements:

```
l1 = left of nums1
r1 = right of nums1
l2 = left of nums2
r2 = right of nums2
```

We want:

```
l1 <= r2
AND
l2 <= r1
```

---

# 🧠 Why This Condition?

Because that ensures:

```
All left elements <= all right elements
```

Which means partition is correct.

---

# 🧪 Dry Run Example

```
nums1 = [1,3,8,9,15]
nums2 = [7,11,18,19,21,25]
```

Total = 11 → odd

---

### Suppose:

```
cut1 = 2
cut2 = 4
```

Left side:

```
1 3 | 8 9 15
7 11 18 19 | 21 25
```

l1 = 3  
l2 = 19  
r1 = 8  
r2 = 21  

Check:

```
3 <= 21 ✅
19 <= 8 ❌
```

Wrong partition.

Move binary search right.

---

### Try:

```
cut1 = 3
cut2 = 3
```

Now:

l1 = 8  
l2 = 18  
r1 = 9  
r2 = 19  

Check:

```
8 <= 19 ✅
18 <= 9 ❌
```

Still wrong.

---

Eventually correct partition found:

Median = max(l1, l2)

---

# 🔥 Why MIN_VALUE and MAX_VALUE?

Edge case when:

```
cut1 = 0
```

Means no element on left from nums1.

So:

```
l1 = -∞
```

Similarly when:

```
cut1 = n1
```

No element on right → r1 = +∞

This avoids out-of-bounds checks.

---

# 🧩 Even Case Formula

If total length is even:

```
Median = ( max(l1,l2) + min(r1,r2) ) / 2
```

---

# ⏱ Time Complexity

```
O(log(min(n1,n2)))
```

Because we binary search smaller array.

---

# 🔥 Why We Always Binary Search Smaller Array?

Because:

```
cut1 ranges from 0 to n1
```

If n1 is small → fewer iterations.

---

# 🏆 Pattern Recognition

If problem says:

```
Two sorted arrays
Median
Logarithmic time
```

Immediately think:

```
Binary Search on Partition
```

---

# 🧠 Final Mental Model

We are NOT searching median directly.

We are searching:

```
Correct partition position
```

Once partition correct:

Median becomes automatic.

---

Bro this is HARD level concept 🔥  
If you understand this fully,

you crossed:

```
Advanced Binary Search Level
```



