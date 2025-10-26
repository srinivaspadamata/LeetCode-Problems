Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.  
  
According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node  
in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”  
  
Example 1:  
![lca 1](Images/lca1.png)  
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1  
Output: 3  
Explanation: The LCA of nodes 5 and 1 is 3.  
  
Example 2:  
![lca 2](Images/lca2.png)  
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4  
Output: 5  
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.  
  
Example 3:  

Input: root = [1,2], p = 1, q = 2  
Output: 1  
  
Constraints:  
The number of nodes in the tree is in the range [2, 105].  
-109 <= Node.val <= 109  
All Node.val are unique.  
p != q  
p and q will exist in the tree.  
  
Code: Java  
  
Time Complexity: O(n)  
Space Complexity: O(h)  
  
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        // 1️⃣ Base case: if root is null or matches p/q, return it
        if(root == null || root == p || root == q) return root;

        // 2️⃣ Search in left and right subtrees
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);

        // 3️⃣ If both left and right found something → current is LCA
        if(left != null && right != null) return root;

        // 4️⃣ Otherwise return whichever side is non-null
        return (left != null) ? left : right;
    }
}
```
