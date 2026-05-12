# 1248. Count Number of Nice Subarrays

---

## 1. 🧠 Problem Understanding (in Simple Words)

You are given an integer array `nums` and an integer `k`.

A subarray is called **nice** if it contains exactly `k` odd numbers.

Your task is to count how many such subarrays exist.

### Example

```text
nums = [1,1,2,1,1], k = 3
```

Nice subarrays:

```text
[1,1,2,1]
[1,2,1,1]
```

Answer:

```text
2
```

---

## 2. 🐢 Brute Force Approach

### Idea

Generate every possible subarray and count how many odd numbers it contains.

### Steps

1. Start from every index `i`.
2. Extend to every index `j`.
3. Count odd numbers.
4. If count becomes `k`, increment answer.

### Drawback

Very slow for large arrays.

---

## 3. 🚀 Optimal Approach (Sliding Window + At Most Technique)

### Key Formula

```text
Exactly(k) = AtMost(k) - AtMost(k - 1)
```

Where:

* `AtMost(k)` = number of subarrays containing at most `k` odd numbers.

So:

* Count all subarrays with ≤ `k` odd numbers.
* Subtract all subarrays with ≤ `k-1` odd numbers.
* The remainder contains exactly `k` odd numbers.

---

## 4. 💡 Why This Approach Works

Suppose:

* `AtMost(3)` includes subarrays with 0, 1, 2, and 3 odd numbers.
* `AtMost(2)` includes subarrays with 0, 1, and 2 odd numbers.

Subtracting removes all cases with fewer than 3 odd numbers, leaving only those with exactly 3.

---

## 5. 🔍 Step-by-Step Dry Run

### Input

```text
nums = [1,1,2,1,1]
k = 3
```

---

### Calculate `AtMost(3)`

Count all subarrays having at most 3 odd numbers.

Result:

```text
14
```

### Calculate `AtMost(2)`

Count all subarrays having at most 2 odd numbers.

Result:

```text
12
```

### Final Answer

```text
Exactly(3) = 14 - 12 = 2
```

---

## 6. 💻 Java Code with Detailed Comments

```java
class Solution {

    public int numberOfSubarrays(int[] nums, int k) {
        // Exactly k odds = AtMost(k) - AtMost(k - 1)
        return atMost(nums, k) - atMost(nums, k - 1);
    }

    private int atMost(int[] nums, int k) {
        // If k is negative, no valid subarray exists
        if (k < 0) return 0;

        int left = 0;
        int count = 0;

        // Expand the right pointer
        for (int right = 0; right < nums.length; right++) {

            // If current number is odd, consume one odd allowance
            if (nums[right] % 2 == 1) {
                k--;
            }

            // Too many odd numbers -> shrink window
            while (k < 0) {
                if (nums[left] % 2 == 1) {
                    k++;
                }
                left++;
            }

            // All subarrays ending at 'right' are valid
            count += right - left + 1;
        }

        return count;
    }
}
```

---

## 7. ⏱️ Time and Space Complexity

| Complexity | Value  |
| ---------- | ------ |
| Time       | `O(n)` |
| Space      | `O(1)` |

We scan the array twice (`atMost(k)` and `atMost(k-1)`), which is still linear time.

---

## 8. 🧩 Pattern Used and How to Recognize It

### Pattern

**Sliding Window + At Most Technique**

### Recognition Clues

Look for phrases like:

* Exactly `k` occurrences
* Exactly `k` odd numbers
* Exactly `k` distinct elements
* Count number of subarrays

### Key Formula

```text
Exactly(k) = AtMost(k) - AtMost(k - 1)
```

Use this whenever:

* You need to count subarrays with exactly `k` properties.
* Counting “at most” can be done efficiently with a sliding window.

---

## 9. 🔗 Similar LeetCode Problems

* 930. Binary Subarrays With Sum
* 992. Subarrays with K Different Integers
* 1358. Number of Substrings Containing All Three Characters
* 713. Subarray Product Less Than K

---

## 10. ⚠️ Common Mistakes to Avoid

### ❌ Forgetting the Formula

```text
Exactly(k) = AtMost(k) - AtMost(k - 1)
```

### ❌ Not Handling `k < 0`

When `k - 1` becomes negative, return `0`.

### ❌ Incorrect Counting

Always add:

```java
count += right - left + 1;
```

because all subarrays ending at `right` and starting from `left` to `right` are valid.

### ❌ Misidentifying Odd Numbers

Use:

```java
nums[i] % 2 == 1
```

---

# 🏆 Final Takeaway

This problem is one of the best examples of the **At Most Sliding Window Technique**.

> **If a problem asks for exactly `k` occurrences in subarrays, think immediately:**
>
> `Exactly(k) = AtMost(k) - AtMost(k - 1)`

Master this pattern, and many advanced sliding window problems become much easier. 🚀🔥
