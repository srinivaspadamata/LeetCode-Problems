Given a binary tree, find its minimum depth.  
The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.  
Note: A leaf is a node with no children.  
  
Example 1:  
![min depth](Images/mindepth.jpg)  
Input: root = [3,9,20,null,null,15,7]  
Output: 2  
  
Example 2:  
Input: root = [2,null,3,null,4,null,5,null,6]  
Output: 5  
  
Constraints:  
The number of nodes in the tree is in the range [0, 105].  
-1000 <= Node.val <= 1000  

Code: Java
  
Time Complexity: O(n)  
Space Compelxity: O(w), w is the width of the binary tree  
  
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
    public int minDepth(TreeNode root) {
        if(root == null) return 0;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        int depth = 1;

        while(!queue.isEmpty()){
            int n = queue.size();
            for(int i=0; i<n; i++){
                TreeNode curr = queue.poll();

                if(curr.left == null && curr.right == null) return depth;

                if(curr.left != null) queue.add(curr.left);
                if(curr.right != null) queue.add(curr.right);
            }
            depth++;
        }
        return depth;
    }
}
```
