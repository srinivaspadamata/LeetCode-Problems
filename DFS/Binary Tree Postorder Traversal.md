Given the root of a binary tree, return the postorder traversal of its nodes' values.  
  
Example 1:  
Input: root = [1,null,2,3]  
Output: [3,2,1]  
Explanation:  
![post order 1](Images/preorder1.png)  
  
Example 2:  
Input: root = [1,2,3,4,5,null,8,null,null,6,7,9]  
Output: [4,6,7,5,2,9,8,3,1]  
Explanation:  
![post order 2](Images/preorder2.png)  
  
Example 3:  
Input: root = []  
Output: []  
  
Example 4:  
Input: root = [1]  
Output: [1]  
  
Constraints:  
The number of the nodes in the tree is in the range [0, 100].  
-100 <= Node.val <= 100  
  
Follow up: Recursive solution is trivial, could you do it iteratively?  
  
Code: Java  
  
**Recursive Code:**  
Time Complexity: O(n)  
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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> binaryTree = new ArrayList<>();
        postOrder(root, binaryTree);
        return binaryTree;
    }

    private void postOrder(TreeNode root, List<Integer> binaryTree){
        if(root == null) return;

        postOrder(root.left, binaryTree);
        postOrder(root.right, binaryTree);
        binaryTree.add(root.val);
    }
}
```

**Iterative Code:** Using Stack and LinkedList  
Time Complexity: O(n)  
Space Complexity: O(h)  

```
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        LinkedList<Integer> result = new LinkedList<>();
        if (root == null) return result;

        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);

        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            // Add to front
            result.addFirst(node.val);

            // Push left first, then right
            if (node.left != null) stack.push(node.left);
            if (node.right != null) stack.push(node.right);
        }

        return result;
    }
}

```
