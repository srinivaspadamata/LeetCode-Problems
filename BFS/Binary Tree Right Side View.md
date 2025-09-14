Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

Example 1:

Input: root = [1,2,3,null,5,null,4]

Output: [1,3,4]

Explanation:

![right view 1](Images/rightview1.png)


Example 2:

Input: root = [1,2,3,4,null,null,null,5]

Output: [1,3,4,5]

Explanation:

![right view 2](Images/rightview2.png)


Example 3:

Input: root = [1,null,3]

Output: [1,3]


Example 4:

Input: root = []

Output: []

Constraints:
The number of nodes in the tree is in the range [0, 100].
-100 <= Node.val <= 100

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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> rightView = new ArrayList<>();
        if(root == null) return rightView;
        Queue<TreeNode> queue= new LinkedList<>();
        queue.add(root);

        while(!queue.isEmpty()){
            int n = queue.size();
            for(int i=0; i<n; i++){
                TreeNode curr = queue.poll();
                if(i == 0) rightView.add(curr.val);
                if(curr.right != null) queue.add(curr.right);
                if(curr.left != null) queue.add(curr.left);
            }
        }
        return rightView;
    }
}
```
Time Complexity: O(n)

Space Complexity: O(w) (max width of tree)
