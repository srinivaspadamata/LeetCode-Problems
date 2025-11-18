Given two integer arrays inorder and postorder where inorder is the inorder traversal of a binary tree and postorder is the postorder traversal of the same tree, construct and return the binary tree.  
  
Example 1:  
![Construct Tree](Images/constructtree.jpg)  
Input: inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]  
Output: [3,9,20,null,null,15,7]  
  
Example 2:  
Input: inorder = [-1], postorder = [-1]  
Output: [-1]  
  
Constraints:  
1 <= inorder.length <= 3000  
postorder.length == inorder.length  
-3000 <= inorder[i], postorder[i] <= 3000  
inorder and postorder consist of unique values.  
Each value of postorder also appears in inorder.  
inorder is guaranteed to be the inorder traversal of the tree.  
postorder is guaranteed to be the postorder traversal of the tree.  
  
Code: Java  
  
Time Complexity: O(n)  
Space Complexity: O(n), since hashmap stores all values from inorder array  
  
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
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        HashMap<Integer, Integer> inOrderMap = new HashMap<>();
        for(int i=0; i<inorder.length; i++){
            inOrderMap.put(inorder[i], i);
        }

        return splitTree(postorder, inOrderMap, postorder.length-1, 0, inorder.length-1);
    }

    private TreeNode splitTree(int[] postorder, HashMap<Integer, Integer> inOrderMap, int rootIndex, int left, int right){
        TreeNode root = new TreeNode(postorder[rootIndex]);
        int mid = inOrderMap.get(postorder[rootIndex]);
        if(mid < right){
            root.right = splitTree(postorder, inOrderMap, rootIndex-1, mid+1, right);
        }
        if(left < mid){
            int rightSize = right - mid;
            root.left = splitTree(postorder, inOrderMap, rootIndex-1-rightSize, left, mid-1);
        }
        return root;
    }
}
```
