Given a binary tree, determine if it is height-balanced.  
  
Example 1:  
![balaced tree 1](Images/balancetree1.jpg)  
Input: root = [3,9,20,null,null,15,7]  
Output: true  
  
Example 2:  
![balaced tree 2](Images/balancetree2.jpg)  
Input: root = [1,2,2,3,3,null,null,4,4]  
Output: false  
  
Example 3:  
Input: root = []  
Output: true  
  
Constraints:  
The number of nodes in the tree is in the range [0, 5000].  
-104 <= Node.val <= 104  
  
Code: Java  
  
**Brute Force:**  
Time Complexity: O(n^2)  
Space Compelxity: O(h)  
  
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean isBalanced(TreeNode root) {
        if(root == null) return true;
        int leftDepth = treeHeight(root.left);
        int rightDepth = treeHeight(root.right);
        if(Math.abs(rightDepth - leftDepth) > 1) return false;
        
        return isBalanced(root.left) && isBalanced(root.right);
    }

    private int treeHeight(TreeNode root){
        if(root == null) return 0;
        return 1 + Math.max(treeHeight(root.left), treeHeight(root.right));
    }
}
```

**Optimized Code:**  
Time Complexity: O(n)  
Space Compelxity: O(h)  

```
class Solution {
    public boolean isBalanced(TreeNode root) {
        return checkHeight(root) != -1;
    }
    private int checkHeight(TreeNode node) {
        if (node == null) return 0;

        int left = checkHeight(node.left);
        if (left == -1) return -1; // Left not balanced

        int right = checkHeight(node.right);
        if (right == -1) return -1; // Right not balanced

        if (Math.abs(left - right) > 1) return -1; // Current not balanced

        return 1 + Math.max(left, right);
    }
}

```
