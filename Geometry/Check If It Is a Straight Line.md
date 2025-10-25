You are given an integer array coordinates, coordinates[i] = [x, y], where [x, y] represents the coordinate of a point. Check if these points make a straight line in the XY plane.  
  
Example 1:  
![straight line 1](Images/straightline1.jpg)  
Input: coordinates = [[1,2],[2,3],[3,4],[4,5],[5,6],[6,7]]  
Output: true  
  
Example 2:  
![straight line 2](Images/straightline2.jpg)  
Input: coordinates = [[1,1],[2,2],[3,4],[4,5],[5,6],[7,7]]  
Output: false  
  
Constraints:  
2 <= coordinates.length <= 1000  
coordinates[i].length == 2  
-10^4 <= coordinates[i][0], coordinates[i][1] <= 10^4  
coordinates contains no duplicate point.  

Code: Java  

Time Complexity: O(n)  
Space Complexity: O(1)  
  
```
class Solution {
    public boolean checkStraightLine(int[][] coordinates) {
        int n = coordinates.length;
        int x1 = coordinates[0][0], y1 = coordinates[0][1];
        int x2 = coordinates[1][0], y2 = coordinates[1][1];

        for(int i=2; i<n; i++){
            int x3 = coordinates[i][0], y3 = coordinates[i][1];
            if((y2-y1)*(x3-x1) != (x2-x1)*(y3-y1)) return false;
        }
        return true;
    }
}
```
