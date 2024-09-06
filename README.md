# 🧩 **LeetCode Challenges**

## **3217. Delete Nodes From Linked List Present in Array**  
**Difficulty**: _Medium_

---

### 📝 **Problem Description**:
You are given:
- An array of integers `nums` 
- The head of a linked list.

Your task is to **return the head of the modified linked list** after removing all nodes that have a value existing in `nums`.

---

### 📋 **Constraints**:
- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^5`
- All elements in `nums` are **unique**.
- The number of nodes in the linked list is within the range `[1, 10^5]`.
- `1 <= Node.val <= 10^5`.
- The input is generated such that there is at least one node in the linked list that has a value **not present** in `nums`.

---

### 🧑‍💻 **Solution in Python**:

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def delNum(self, head, banned):
        while head.next and len(banned) > head.next.val and banned[head.next.val]:
            head.next = head.next.next
        if head.next: 
            self.delNum(head.next, banned)

    def modifiedList(self, nums: List[int], head: Optional[ListNode]) -> Optional[ListNode]:
        fake_head = ListNode(0, head)
        banned = [False] * (max(nums) + 1)
        
        # Mark nodes in nums as banned
        for num in nums: 
            banned[num] = True
            
        # Recursively delete nodes
        self.delNum(fake_head, banned)
        
        return fake_head.next
```

---

### ⚙️ **Explanation**:

1. **Helper Function (`delNum`)**:
   - Recursively traverses the linked list and removes any node whose value is in `banned`.
   
2. **Main Function (`modifiedList`)**:
   - Creates a dummy node (`fake_head`) to handle edge cases.
   - Uses a boolean array `banned` to track whether a node's value should be removed.
   - Iterates over `nums` to mark the nodes to be removed.
   - Recursively modifies the linked list by calling `delNum`.

---

### 🧠 **Key Concepts**:
- **Linked List Manipulation**: Directly altering pointers to skip over nodes that need to be deleted.
- **Recursive Approach**: Efficient handling of linked list traversal and deletion in-place.
- **Time Complexity**: O(n + m) where `n` is the length of the linked list and `m` is the length of the `nums` array.

---

