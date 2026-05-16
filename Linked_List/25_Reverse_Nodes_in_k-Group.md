# 🔄 Reverse Nodes in k-Group 
### Pattern : (In-place Reversal of a LinkedList)

---

## 📌 Problem

Given a linked list, reverse the nodes of the list `k` at a time.

Rules:

- Reverse every group of exactly `k` nodes.
- If remaining nodes are fewer than `k`, leave them unchanged.
- Only node links are changed, not values.

---

## ✅ Example

Input:

```text
head = 1 → 2 → 3 → 4 → 5
k = 2
```

Output:

```text
2 → 1 → 4 → 3 → 5
```

---

## ✅ Code (UNCHANGED)

```java
class Solution {
    public ListNode reverseLinkedList(ListNode curr){
        if(curr == null || curr.next == null){
            return curr;
        }

        ListNode newHead = reverseLinkedList(curr.next);
        curr.next.next = curr;
        curr.next = null;
        return newHead;
    }

    public ListNode getKthNode(ListNode temp,int k){
        k = k - 1;
        while(temp != null && k>0){
            temp = temp.next;
            k--;
        }

        return temp;
    }

    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode temp = head;
        ListNode prevLast = null;

        while(temp != null){

            ListNode kThNode = getKthNode(temp,k);
            if(kThNode == null){
                if(prevLast != null) prevLast.next = temp;
                break;
            }

            ListNode nextNode = kThNode.next;
            kThNode.next = null;

            ListNode newHead = reverseLinkedList(temp);

            if(temp == head){
                head = newHead;
            }else{
                prevLast.next = newHead;
            }

            prevLast = temp;
            temp = nextNode;
        }

        return head;
    }
}
```

---

# 🧠 High-Level Strategy

For every group of `k` nodes:

1. Find the `k`th node.
2. If fewer than `k` nodes remain → stop.
3. Save the next group's starting node.
4. Cut the current group.
5. Reverse the current group.
6. Connect with previous reversed group.
7. Move to the next group.

---

# 🎯 Core Mental Model

```text
[temp ... kThNode] | nextNode
        ↓
      reverse
        ↓
[newHead ... temp] | nextNode
```

After reversal:

- `newHead` = start of reversed group
- `temp` = end of reversed group

---

# 🔍 Helper 1: `getKthNode()`

```java
public ListNode getKthNode(ListNode temp,int k)
```

Returns the `k`th node starting from `temp`.

---

## Example

```text
temp = 1 → 2 → 3 → 4
k = 3
```

Returns node:

```text
3
```

---

# 🔍 Helper 2: `reverseLinkedList()`

Recursively reverses a linked list and returns the new head.

---

## Example

```text
1 → 2 → 3
```

Becomes:

```text
3 → 2 → 1
```

---

# 🔄 Main Loop Variables

| Variable | Meaning |
|------:|---------|
| `temp` | Start of current group |
| `kThNode` | Last node of current group |
| `nextNode` | Start of next group |
| `newHead` | Head after reversing current group |
| `prevLast` | Tail of previous reversed group |

---

# ✂️ Step 1: Find k-th Node

```java
ListNode kThNode = getKthNode(temp,k);
```

If `null`, there are fewer than `k` nodes left.

---

# 🔌 Step 2: Save Next Group

```java
ListNode nextNode = kThNode.next;
```

---

# ✂️ Step 3: Cut Current Group

```java
kThNode.next = null;
```

Now the group becomes an independent linked list.

---

# 🔄 Step 4: Reverse Current Group

```java
ListNode newHead = reverseLinkedList(temp);
```

---

# 🔗 Step 5: Connect with Previous Group

### First Group

```java
head = newHead;
```

### Other Groups

```java
prevLast.next = newHead;
```

---

# 📍 Step 6: Update Pointers

```java
prevLast = temp;
temp = nextNode;
```

After reversal, `temp` becomes the tail of the reversed group.

---

# 🧪 Dry Run

Input:

```text
1 → 2 → 3 → 4 → 5
k = 2
```

---

## Group 1: `1 → 2`

Reverse:

```text
2 → 1
```

List:

```text
2 → 1
```

`prevLast = 1`

---

## Group 2: `3 → 4`

Reverse:

```text
4 → 3
```

Connect:

```text
2 → 1 → 4 → 3
```

`prevLast = 3`

---

## Remaining: `5`

Less than `k`, so leave unchanged.

Final:

```text
2 → 1 → 4 → 3 → 5
```

---

# 🧠 Why `prevLast = temp`

Before reversal:

```text
temp = first node of group
```

After reversal:

```text
temp = last node of reversed group
```

This tail is needed to connect to the next reversed group.

---

# ⏱ Complexity

### Time

```text
O(n)
```

Each node is visited a constant number of times.

### Space

Recursive reversal uses:

```text
O(k)
```

recursion stack for each group.

---

# 🏆 Pattern Recognition

If a linked list problem requires:

- Processing fixed-size chunks
- Reversing segments
- Reconnecting parts

Think:

```text
Find boundary → Cut → Reverse → Reconnect
```
