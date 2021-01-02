# Find a Corresponding Node of a Binary Tree in a Clone of That Tree

Given two binary trees `original` and `cloned` and given a reference to a node `target` in the original tree.

The `cloned` tree is a **copy of** the `original` tree.

Return _a reference to the same node_ in the `cloned` tree.

**Note** that you are **not allowed** to change any of the two trees or the `target` node and the answer **must be** a reference to a node in the `cloned` tree.

### 思路：

dfs traverse整个树，如果发现target，返回。

### Code：

```java

class Solution {
    public final TreeNode getTargetCopy(final TreeNode original, final TreeNode cloned, final TreeNode target) {
        return dfs(cloned, target);
    }
    public TreeNode dfs(TreeNode root, TreeNode target){
        if(root == null) return null;
        if(root.val == target.val) return root;
        
        TreeNode left = dfs(root.left, target);
        if(left != null) return left;
        TreeNode right = dfs(root.right, target);
        return right == null ? null : right;
        
    }
}
```

