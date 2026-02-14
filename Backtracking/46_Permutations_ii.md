# 🔁 Permutations II (Unique Permutations – Duplicate Handling Explained)

---

## 📌 Problem

Given an array `nums` that may contain duplicates,  
return **all unique permutations**.

---

## 🧠 Core Idea

We:

1️⃣ Sort the array  
2️⃣ Use a `boolean[] used` to track visited elements  
3️⃣ Skip duplicate branches carefully  

---

# 💻 Code (Important Part)

```java
if (i > 0 && nums[i] == nums[i-1] && !used[i-1]) continue;
```

This line prevents duplicate permutations.

---

# 🧨 Why Duplicates Happen?

Example:

```
nums = [1,1,2]
```

If we don't handle duplicates, we may generate:

```
[1,1,2]
[1,1,2]  ❌ duplicate
[1,2,1]
[1,2,1]  ❌ duplicate
...
```

We need to block duplicate branches at the SAME recursion level.

---

# 🔍 Break Down the Condition

```
if (i > 0 && nums[i] == nums[i-1] && !used[i-1])
```

Let’s understand each part:

---

## 1️⃣ `i > 0`

Prevents out-of-bound access when checking `nums[i-1]`.

---

## 2️⃣ `nums[i] == nums[i-1]`

Checks if current element is same as previous element.

Since we sorted the array:

```
Duplicate values are adjacent.
```

Example:
```
[1,1,2]
```

---

## 3️⃣ `!used[i-1]`

This is the most important part.

It means:

> If previous duplicate element is NOT used in current recursion path,
> then skip this one.

---

# 🧠 Why `!used[i-1]` Works?

It ensures:

We only use the FIRST duplicate at a given recursion level.

---

# 🎨 Visual Explanation

Example:

```
nums = [1,1,2]
```

Sorted:
```
Index:  0 1 2
Value:  1 1 2
```

---

## 🔹 Case 1: First 1 used

Path:
```
[1]
```

Now `used[0] = true`

At next level:

Second `1` can be used because:

```
used[i-1] == true
```

So condition fails → allowed.

✔ Valid case.

---

## 🔹 Case 2: First 1 NOT used

At same recursion level:

If we try second `1` first:

```
used[0] = false
```

Condition becomes:

```
i > 0 ✔
nums[i] == nums[i-1] ✔
!used[i-1] ✔
```

So we skip.

This prevents duplicate permutation branch.

---

# 🔥 What This Actually Prevents

It prevents:

```
Picking duplicate elements in the same tree level
```

But allows:

```
Using duplicates in different tree depths
```

Very important difference.

---

# 🌳 Tree Visualization

Without skip:

```
Level 1:
  pick 1(index 0)
  pick 1(index 1) ❌ duplicate branch
```

With skip:

```
Level 1:
  pick 1(index 0)
  skip 1(index 1)
```

Duplicate branch eliminated.

---

# 🧠 Short Memory Trick

👉 "Skip duplicate if previous identical element was NOT used"

That means:

```
Only allow duplicate if previous duplicate was chosen first.
```

---
# Java
```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {

        Arrays.sort(nums);
        List<List<Integer>> list = new ArrayList<>();
        boolean[] used = new boolean[nums.length];

        backtrack(list,new ArrayList<>(),nums,used);
        return list;
        
    }

    private void backtrack(List<List<Integer>> list,List<Integer> tempList,int[] nums,boolean[] used){

        if(tempList.size() == nums.length){
            list.add(new ArrayList<>(tempList));
            return;
        }else{

            for(int i = 0;i<nums.length;i++){
                if(used[i]) continue;

                 // skip duplicates
                 if (i > 0 && nums[i] == nums[i-1] && !used[i-1]) continue;
                
                used[i] = true;
                tempList.add(nums[i]);
                backtrack(list,tempList,nums,used);

                used[i] = false;
                tempList.remove(tempList.size() - 1);
            }
        }
    }
}
```

# ⏱ Time Complexity

Worst case:
```
O(n × n!)
```

But duplicates reduce actual permutations.

---

# 📦 Space Complexity

```
O(n)
```

For recursion + used array.

---

# 🏆 Final Summary

Condition:

```java
if (i > 0 && nums[i] == nums[i-1] && !used[i-1]) continue;
```

Means:

```
If this element is same as previous
AND previous was not chosen in this path
→ Skip to avoid duplicate permutation.
```

---

# ✅ Final Insight

This pattern is used in:

- Permutations II
- Combination Sum II
- Subsets II

Master this condition → you master duplicate handling in backtracking.

---


