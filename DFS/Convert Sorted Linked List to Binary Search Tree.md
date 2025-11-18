Given the head of a singly linked list where elements are sorted in ascending order, convert it to a height-balanced binary search tree.  
  
Example 1:  
![LinkedListToBST](Images/linkedBST.jpg)  
Input: head = [-10,-3,0,5,9]  
Output: [0,-3,9,-10,null,5]  
Explanation: One possible answer is [0,-3,9,-10,null,5], which represents the shown height balanced BST.  
  
Example 2:  
Input: head = []  
Output: []  
  
Constraints:  
The number of nodes in head is in the range [0, 2 * 104].  
-105 <= Node.val <= 105  
  
Code: Java  
  
**Brute Force:**  
Time Complexity: O(n log n) -> For each recursive level, you scan the list to find the middle element → O(n), Tree height = log n.  
Space Complexity: O(log n) -> Since this builds a balanced BST, its height is log n. recursion depth = log n. 
  
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
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
    public TreeNode sortedListToBST(ListNode head) {
        return constructBST(head, null);
    }

    private TreeNode constructBST(ListNode head, ListNode tail){
        if(head == tail) return null;

        ListNode slow = head, fast = head;
        while(fast != tail && fast.next != tail){
            slow = slow.next;
            fast = fast.next.next;
        }
        TreeNode root = new TreeNode(slow.val);
        root.left = constructBST(head, slow);
        root.right = constructBST(slow.next, tail);

        return root;
    }

    private ListNode middleNode(ListNode head){
        ListNode slow = head, fast = head;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
}
```

**Optimized Code:**  
Time Complexity: O(n)  
Space Complexity: O(log n), recursion depth = log n.  

```
class Solution {

    private ListNode current;

    public TreeNode sortedListToBST(ListNode head) {
        int size = getSize(head);
        current = head;
        return buildBST(0, size - 1);
    }

    private int getSize(ListNode head) {
        int count = 0;
        while (head != null) {
            count++;
            head = head.next;
        }
        return count;
    }

    private TreeNode buildBST(int left, int right) {
        if (left > right) return null;

        int mid = (left + right) / 2;

        // 1. Build left subtree
        TreeNode leftChild = buildBST(left, mid - 1);

        // 2. Node from current LinkedList value
        TreeNode root = new TreeNode(current.val);
        current = current.next;

        // 3. Build right subtree
        TreeNode rightChild = buildBST(mid + 1, right);

        root.left = leftChild;
        root.right = rightChild;

        return root;
    }
}
```
