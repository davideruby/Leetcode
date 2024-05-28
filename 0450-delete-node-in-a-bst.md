## [450. Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/)

<h2 style="color:#fac31d">Medium</h2>
Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.

Basically, the deletion can be divided into two stages:

1. Search for a node to remove.
2. If the node is found, delete the node.

## Solution
```python
class Solution:
    def deleteNode(self, root: Optional[TreeNode], key: int) -> Optional[TreeNode]:
        def findMinNode(root: Optional[TreeNode]) -> Optional[TreeNode]:
            if root.left == None:
                return root
            else:
                return findMinNode(root.left)

        if root == None:
            return None
        
        if key < root.val:
            root.left = self.deleteNode(root.left, key)
        elif key > root.val:
            root.right = self.deleteNode(root.right, key)
        else:
            if root.left == None:
                return root.right
            elif root.right == None:
                return root.left
            else:
                min_node = findMinNode(root.right)
                root.val = min_node.val
                root.right = self.deleteNode(root.right, min_node.val)
        return root
```

## Notes
First of all, we have to find the node to remove. So, if `key < root.val` call the function on `root.left`, otherwise if `key > root.val` call it on `root.right`.
If neither of them, we found the node to remove.

Now, we have 3 cases to handle:
1. The node is a leaf (it has no children), so we can simply return `null`.
2. The node has only 1 child. In this case, we have to return that child.
3. The node has 2 children. Here, we replace the value of the node with the minimum value of the right sub-tree and then we remove the node with the minimum value. Note that the minimum value will fall in one the first two cases. 
and that you can do this same trick with the maximum value of the left sub-tree. 
