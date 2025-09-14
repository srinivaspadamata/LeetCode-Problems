Given the root of a binary tree and an integer targetSum, return the number of paths where the sum of the values along the path equals targetSum.

The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes).

Example 1:

![path sum](Images/pathsum3.jpg)

Input: root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8
Output: 3
Explanation: The paths that sum to 8 are shown.

Example 2:
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
Output: 3

Constraints:

The number of nodes in the tree is in the range [0, 1000].
-109 <= Node.val <= 109
-1000 <= targetSum <= 1000

Code:

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
    public int pathSum(TreeNode root, int targetSum) {
        if(root == null) return 0;
        return pathSumCount(root, targetSum) + pathSum(root.left, targetSum) + pathSum(root.right, targetSum);
    }

    private int pathSumCount(TreeNode node, long targetSum){
        if(node == null) return 0;
        int count = (node.val == targetSum) ? 1 : 0;
        count += pathSumCount(node.left, targetSum - node.val);
        count += pathSumCount(node.right, targetSum - node.val);
        return count;
    }
}
```

Time Complexity: O(n²) (skewed) / O(n log n) (balanced), O(n) -> pathSum() is called for every node, O(n) -> For each node, pathsFrom() explores all paths starting from that node
Space Compelxity: O(h), skewed tree: O(n), where h = height of the tree
