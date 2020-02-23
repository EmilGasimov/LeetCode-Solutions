You are given a perfect binary tree where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

`struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}`

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

 

Follow up:

You may only use constant extra space.
Recursive approach is fine, you may assume implicit stack space does not count as extra space for this problem.

### Solution 1 - Recursive [own]
```java
class Solution {
    public Node connect(Node root) {
        if(root == null) return root;
        if(root.left == null) {
            root.next = null;
            return root;
        }
        
        root.next = null;
        root.left = connect(root.left);
        root.right = connect(root.right);
        Node pred = root.left, succ = root.right;
        while(pred != null) {
            pred.next = succ;
            pred = pred.right;
            succ = succ.left;
        }
                
        return root;
    }
}
```

### Solution 2 - Iterative

```java

class Solution {
    public Node connect(Node root) {
        Node Root = root;
        while(root != null && root.left != null) {
            Node cur = root;
            while(cur != null) {
                cur.left.next = cur.right;
                cur.right.next = cur.next == null? null: cur.next.left;
                cur = cur.next;
            }
            root = root.left;
        }
        return Root;
    }
}



```
