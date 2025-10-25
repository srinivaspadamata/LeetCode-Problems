Given an array of points where points[i] = [xi, yi] represents a point on the X-Y plane, return the maximum number of points that lie on the same straight line.  
  
Example 1:  
![max points 1](Images/maxpoints1.jpg)  
Input: points = [[1,1],[2,2],[3,3]]  
Output: 3  

Example 2:  
![max points 2](Images/maxpoints2.jpg)  
Input: points = [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]  
Output: 4  
  
Constraints:  
1 <= points.length <= 300  
points[i].length == 2  
-104 <= xi, yi <= 104  
All the points are unique.  
  
Code: Java  
  
**Brute Force:**  
Time Complexity: O(n^3)  
Space Complexity: O(1)  
  
```
class Solution {
    public int maxPoints(int[][] points) {
        int n = points.length;
        if(n < 2) return n;
        int maxCount = 0;

        for(int i=0; i<n; i++){
            for(int j=i+1; j<n; j++){
                int count = 2;
                for(int k=0; k<n; k++){
                    if(k != i && k != j){
                        int x1 = points[i][0], y1 = points[i][1];
                        int x2 = points[j][0], y2 = points[j][1];
                        int x3 = points[k][0], y3 = points[k][1];

                        if((y2-y1)*(x3-x1) == (x2-x1)*(y3-y1)){
                            count++;
                        }
                    }
                }
                maxCount = Math.max(maxCount, count);
            }
        }
        return maxCount;
    }
}
```  
If three points are on the same line, then the slope between the first two points (1,2) should be equal to the slope between (1,3).  
so the formula is  
(y2−y1​)/(x2−x1) = (y3−y1)/(x3−x1)​ => (y2-y1)*(x3-x1) == (x2-x1)*(y3-y1)  
int count = 2; => Points i and j are already on that line, so start the count at 2.  
  
**Optimized Code:**  
Time Complexity: O(n^2)  
Space Complexity: O(1)  
  
```
class Solution {
    public int maxPoints(int[][] points) {
        int n = points.length;
        if(n < 2) return n;
        int maxCount = 0;

        for(int i=0; i<n; i++){
            HashMap<String, Integer> slopeMap = new HashMap<>();
            int vertical = 0;
            int duplicates = 1;

            for(int j=i+1; j<n; j++){
                int dx = points[j][0] - points[i][0];
                int dy = points[j][1] - points[i][1];

                if(dx == 0 && dy == 0){
                    duplicates++;
                }
                else if(dx == 0){
                    vertical++;
                }
                else{
                    int gcd = gcd(dy, dx);
                    dx /= gcd;
                    dy /= gcd;
                    if(dx < 0){ dx = -dx; dy = -dy; }
                    String key = dy + "/" + dx;
                    slopeMap.put(key, slopeMap.getOrDefault(key, 0) + 1);
                }
            }
            int currentMax = vertical;
            for(int count: slopeMap.values()) currentMax = Math.max(currentMax, count);
            maxCount = Math.max(maxCount, currentMax + duplicates);
        }
        return maxCount;
    }

    static int gcd(int a, int b){
        if(b == 0) return Math.abs(a);
        return gcd(b, a%b);
    }
}
```  
  
int duplicate = 1; => Counts points identical to the anchor (same x and y). Start at 1 to include the anchor itself.  
if (dx == 0 && dy == 0) duplicate++; => Point j is identical to anchor i. Count it as a duplicate.  
else if (dx == 0) vertical++; => Vertical line through anchor: increment vertical count. If not slope=dy/dx will be infinity.  
Compute g = gcd(dy, dx) and divide: dy /= g; dx /= g; => This reduces the fraction dy/dx to its lowest terms (e.g., 2/4 → 1/2).  
if dx < 0 then flip both signs so dx is positive. => This keeps -1/2 and 1/-2 from being treated as different keys.  
  
