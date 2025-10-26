Given the root of a binary tree, return the bottom-up level order traversal of its nodes' values. (i.e., from left to right, level by level from leaf to root).  
  
Example 1:  
![level order](Images/levelorder.jpg)  
Input: root = [3,9,20,null,null,15,7]  
Output: [[15,7],[9,20],[3]]  
  
Example 2:  
Input: root = [1]  
Output: [[1]]  
  
Example 3:  
Input: root = []  
Output: []  
  
Constraints:  
The number of nodes in the tree is in the range [0, 2000].  
-1000 <= Node.val <= 1000  

Code: Java  
  
Time Complexity: O(n)  
Space Complexity: O(n)  
  
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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        List<List<Integer>> result = new ArrayList<>();
        if(root == null) return result;
        queue.add(root);

        while(!queue.isEmpty()){
            int n = queue.size();
            List<Integer> list = new ArrayList<>();
            for(int i=0; i<n; i++){
                TreeNode curr = queue.poll();
                list.add(curr.val);

                if(curr.left != null) queue.add(curr.left);
                if(curr.right != null) queue.add(curr.right);
            }
            result.addFirst(list);  //result.add(list);
        }
        //Collections.reverse(result);
        return result;
    }
}
```
