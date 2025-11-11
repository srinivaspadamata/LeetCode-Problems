Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.  
  
Example 1:  
![Rain Water Trap](Images/rainwatertrap.png)  
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]  
Output: 6  
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.  
  
Example 2:  
Input: height = [4,2,0,3,2,5]  
Output: 9  
  
Constraints:  
n == height.length  
1 <= n <= 2 * 104  
0 <= height[i] <= 105  
  
Code: Java  
  
**Optimized Approach:**  
Time Complexity: O(n)  
Space Complexity: O(1)  
  
```
class Solution {
    public int trap(int[] height) {
        int left = 0, right = height.length - 1;
        int leftMax = 0, rightMax = 0, water = 0;

        while(left < right){
            if(height[left] < height[right]){
                if(height[left] >= leftMax){
                    leftMax = height[left];
                }
                else{
                    water += leftMax - height[left];
                }
                left++;
            }
            else{
                if(height[right] >= rightMax){
                    rightMax = height[right];
                }
                else{
                    water += rightMax - height[right];
                }
                right--;
            }
        }
        return water;
    }
}
```
  
**Brute Force Approach:**  
Time Complexity: O(n^2)  
Space Complexity: O(1)  
  
```
public class TrappingRainWaterBrute {
    public static int trap(int[] height) {
        int n = height.length;
        int water = 0;

        for (int i = 0; i < n; i++) {
            int leftMax = 0, rightMax = 0;

            // Find max to the left
            for (int j = 0; j <= i; j++) {
                leftMax = Math.max(leftMax, height[j]);
            }

            // Find max to the right
            for (int j = i; j < n; j++) {
                rightMax = Math.max(rightMax, height[j]);
            }

            water += Math.min(leftMax, rightMax) - height[i];
        }
        return water;
    }

    public static void main(String[] args) {
        int[] height = {4,2,0,3,2,5};
        System.out.println("Trapped Water (Brute Force): " + trap(height));
    }
}

```
