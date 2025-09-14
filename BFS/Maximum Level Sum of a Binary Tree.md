Given the root of a binary tree, the level of its root is 1, the level of its children is 2, and so on.  
Return the smallest level x such that the sum of all the values of nodes at level x is maximal.  
  
Example 1:  
![max level sum](maxlevelsum.jfif)  
Input: root = [1,7,0,7,-8,null,null]  
Output: 2  
Explanation:  
Level 1 sum = 1.  
Level 2 sum = 7 + 0 = 7.  
Level 3 sum = 7 + -8 = -1.
So we return the level with the maximum sum which is level 2.  
  
Example 2:  
Input: root = [989,null,10250,98693,-89388,null,null,null,-32127]  
Output: 2  
  
Constraints:  
The number of nodes in the tree is in the range [1, 104].  
-105 <= Node.val <= 105  
  
Code: Java  
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
    public int maxLevelSum(TreeNode root) {
        if(root == null) return 0;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        int maxSum = Integer.MIN_VALUE;
        int level = 0;
        int maxLevel = 1;

        while(!queue.isEmpty()){
            int n = queue.size();
            int levelSum = 0;
            level++;
            
            for(int i=0; i<n; i++){
                TreeNode curr= queue.poll();
                levelSum += curr.val;
                if(curr.left != null) queue.add(curr.left);
                if(curr.right != null) queue.add(curr.right);
            }
            if(levelSum > maxSum){
                maxSum = levelSum;
                maxLevel = level;
            }
        }
        return maxLevel;
    }
}
```
Time Complexity: O(n), each node visited once.  
Space Complexity: O(w), where w is the maximum width of the tree (queue).  
