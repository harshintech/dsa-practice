# 🔄 Permutations (Backtracking)

---

## 📌 Problem

Given an integer array `nums`,  
return **all possible permutations**.

A permutation means:

```
All possible arrangements of elements.
```

---
## Explain With Drawing 🎨
##### Example = [1,2,3]
![permutation.jpg.jpeg](https://assets.leetcode.com/users/images/ac85d2c2-e60e-4a6b-9a96-e760022e0840_1771072633.3824024.jpeg)


---

## 🧩 Example

Input:
```
nums = [1,2,3]
```

Output:
```
[
 [1,2,3],
 [1,3,2],
 [2,1,3],
 [2,3,1],
 [3,1,2],
 [3,2,1]
]
```

Total:
```
3! = 6 permutations
```

---

# 🚀 Approach (Backtracking)

---

## 🔑 Core Idea

For permutations:

At every position,
we try **every unused number**.

Unlike subsets:
- Subsets move forward using `start`
- Permutations try every unused element

---

# 💻 Corrected Java Code

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {

        List<List<Integer>> list = new ArrayList<>();

        backtrack(list, new ArrayList<>(), nums);

        return list;
    }

    private void backtrack(List<List<Integer>> list,
                           List<Integer> tempList,
                           int[] nums){

        if(tempList.size() == nums.length){
            list.add(new ArrayList<>(tempList));
            return;
        }

        for(int i = 0; i < nums.length; i++){

            if(tempList.contains(nums[i]))
                continue;

            tempList.add(nums[i]);

            backtrack(list, tempList, nums);

            tempList.remove(tempList.size() - 1);
        }
    }
}
```

---

# 🌳 Decision Tree Visualization

For `[1,2,3]`:

```
              []
         /       |       \
       1         2         3
     /   \     /   \     /   \
   2     3   1     3   1     2
  /       \  /       \  /       \
 3         2 3         1 2         1
```

Each full branch = one permutation.

---

# 🧠 Dry Run

Input:
```
[1,2]
```

Step 1:
```
[]
```

Pick 1:
```
[1]
```

Pick 2:
```
[1,2]
```

Backtrack:
```
[1]
```

Backtrack:
```
[]
```

Pick 2:
```
[2]
```

Pick 1:
```
[2,1]
```

---

# ⏱ Time Complexity

Total permutations:

```
n!
```

Each permutation takes O(n) to copy.

Total:

```
O(n × n!)
```

---

# 📦 Space Complexity

Recursion stack:
```
O(n)
```

Result storage:
```
O(n × n!)
```

---

# 🔥 Important Difference

| Subsets | Permutations |
|----------|--------------|
| Use start index | No start index |
| Include/Exclude | Try every unused |
| Total = 2^n | Total = n! |

---

# ⚠ Optimization Tip

Using:

```
tempList.contains(nums[i])
```

Costs O(n).

Better approach:

Use a boolean[] visited array:

```
boolean[] used = new boolean[n];
```

Then check in O(1).

---

# 🏆 Pattern Used

Backtracking  
Choice Exploration  
Used Element Tracking  

---

# ✅ Final Output

Input:
```
[1,2,3]
```

Output:
```
6 permutations
```

---


