Given the root of a binary tree, determine if it is a valid binary search tree (BST).  
  
A valid BST is defined as follows:  
  
The left subtree of a node contains only nodes with keys strictly less than the node's key.  
The right subtree of a node contains only nodes with keys strictly greater than the node's key.  
Both the left and right subtrees must also be binary search trees.  
  
Example 1:  
[!valid bst 1](Images/validbst1.jpg)  
Input: root = [2,1,3]  
Output: true  
  
Example 2:  
[!valid bst 2](Images/validbst2.jpg)  
Input: root = [5,1,4,null,null,3,6]  
Output: false  
Explanation: The root node's value is 5 but its right child's value is 4.  
  
Constraints:  
The number of nodes in the tree is in the range [1, 104].  
-231 <= Node.val <= 231 - 1  
  
Code: Java  
  
Brute Force:  
Time Complexity: O(n)  
Space Complexity: O(n), due to array list  
  
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
    public boolean isValidBST(TreeNode root) {
        List<Integer> inOrder = new ArrayList<>();
        inOrder(root, inOrder);

        for(int i=1; i<inOrder.size(); i++){
            if(inOrder.get(i) <= inOrder.get(i-1)){
                return false;
            }
        }
        return true;
    }

    static void inOrder(TreeNode root, List<Integer> inOrder){
        if(root == null) return;
        inOrder(root.left, inOrder);
        inOrder.add(root.val);
        inOrder(root.right, inOrder);
    }
}
```  
  
Optimized Code:  
Time Complexity: O(n)  
Space Complexity: O(h), h is the height or depth of the tree  
  
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
    public boolean isValidBST(TreeNode root) {
        return validBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean validBST(TreeNode root, long min, long max){
        if(root == null) return true;
        if(root.val <= min || root.val >= max) return false;
        return validBST(root.left, min, root.val) && validBST(root.right, root.val, max);
    }
}
```  
