# Find Root of N-Ary Tree



You are given all the nodes of an [**N-ary tree**](https://leetcode.com/articles/introduction-to-n-ary-trees/) as an array of `Node` objects, where each node has a **unique value**.

Return _the **root** of the N-ary tree_.

**Custom testing:**

An N-ary tree can be serialized as represented in its level order traversal where each group of children is separated by the `null` value \(see examples\).

![](https://assets.leetcode.com/uploads/2019/11/08/sample_4_964.png)

For example, the above tree is serialized as `[1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]`.

The testing will be done in the following way:

1. The **input data** should be provided as a serialization of the tree.
2. The driver code will construct the tree from the serialized input data and put each `Node` object into an array **in an arbitrary order**.
3. The driver code will pass the array to `findRoot`, and your function should find and return the root `Node` object in the array.
4. The driver code will take the returned `Node` object and serialize it. If the serialized value and the input data are the **same**, the test **passes**.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/12/narytreeexample.png)

```text
Input: tree = [1,null,3,2,4,null,5,6]
Output: [1,null,3,2,4,null,5,6]
Explanation: The tree from the input data is shown above.
The driver code creates the tree and gives findRoot the Node objects in an arbitrary order.
For example, the passed array could be [Node(5),Node(4),Node(3),Node(6),Node(2),Node(1)] or [Node(2),Node(6),Node(1),Node(3),Node(5),Node(4)].
The findRoot function should return the root Node(1), and the driver code will serialize it and compare with the input data.
The input data and serialized Node(1) are the same, so the test passes.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/11/08/sample_4_964.png)

```text
Input: tree = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
Output: [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
```

### 题意:

给你一个list of treenode 让你找出这个tree的总root node。这个tree里所以的val都是unique的。

### 思路:

**解法\#1: O\(n\) space**

建一个hashset， iterate一遍整个list， 把里面node的children 加到set里

再遍历一遍list，return 不在set里的那个node。

**解法\#2 : O\(1\) space**

因为这个tree里所以的value都是unique的，所以我们可以用sum。把node的值加一起，再减去所以children的值，剩下的就是root的值。 再iterate一遍list 找和root值相等的node并返回。

**解法\#3: O\(1\) space**

与其用+ - 去找出root， 我们可以用xor， 因为除了root之外，其他的node都被visit了2次。

```java
class Solution {
    public Node findRoot(List<Node> tree) {
        if(tree.size() == 0) return null;
        int root = 0;
        for(Node node : tree) {
            root ^= node.val;
            for(Node child : node.children) {
                root ^= child.val;
            }
        }
        for(Node node : tree) {
            if(node.val == root) {
                return node;
            }
        }
        return null;
    }
}
```

