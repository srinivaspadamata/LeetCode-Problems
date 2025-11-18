You are given the root of a binary search tree (BST), where the values of exactly two nodes of the tree were swapped by mistake. Recover the tree without changing its structure.  
  
Example 1:  
![Recover BST 1](Images/recover1.jpg)  
Input: root = [1,3,null,null,2]  
Output: [3,1,null,null,2]  
Explanation: 3 cannot be a left child of 1 because 3 > 1. Swapping 1 and 3 makes the BST valid.  
  
Example 2:  
![Recover BST 2](Images/recover2.jpg)  
Input: root = [3,1,4,null,null,2]  
Output: [2,1,4,null,null,3]  
Explanation: 2 cannot be in the right subtree of 3 because 2 < 3. Swapping 2 and 3 makes the BST valid.  
  
Constraints:  
The number of nodes in the tree is in the range [2, 1000].  
-231 <= Node.val <= 231 - 1  
  
Follow up: A solution using O(n) space is pretty straight-forward. Could you devise a constant O(1) space solution?  
  
Code: Java  
  
Time Complexity: O(n)  
Space Complexity: O(h), where h is the height of the tree  
  
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
    private TreeNode first = null, second = null, prev = null;
    public void recoverTree(TreeNode root) {
        inOrder(root);
        
        int temp = first.val;
        first.val = second.val;
        second.val = temp;
    }

    private void inOrder(TreeNode root){
        if(root == null) return;

        inOrder(root.left);

        if(prev != null && prev.val > root.val){
            if(first == null) first = prev;
            second = root;
        }
        prev = root;

        inOrder(root.right);
    }
}
```
  
Inorder: 1 5 3 4 2 6  
prev=1, curr=5 → OK  
prev=5, curr=3 → violation → first = 5, second = 3  
prev=3, curr=4 → OK  
prev=4, curr=2 → violation → second = 2  
swap(first, second) → swap(5, 2) -> 1 2 3 4 5 6  
