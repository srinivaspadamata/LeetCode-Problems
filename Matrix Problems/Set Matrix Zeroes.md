Given an m x n integer matrix matrix, if an element is 0, set its entire row and column to 0's.  
You must do it in place.  
  
Example 1:  
![Zero Matrix 1](Images/zeromatrix1.jpg)  
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]  
Output: [[1,0,1],[0,0,0],[1,0,1]]  
  
Example 2:  
![Zero Matrix 2](Images/zeromatrix2.jpg)  
Input: matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]  
Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]  
  
Constraints:  
m == matrix.length  
n == matrix[0].length  
1 <= m, n <= 200  
-231 <= matrix[i][j] <= 231 - 1  
  
Follow up:  
A straightforward solution using O(mn) space is probably a bad idea.  
A simple improvement uses O(m + n) space, but still not the best solution.  
Could you devise a constant space solution?  
  
Code: Java  
  
Time Complexity: O(m × n), where m, n are number of rows and columns  
Space Complexity: O(1)  
  
```
class Solution {
    public void setZeroes(int[][] matrix) {
        int m = matrix.length, n = matrix[0].length;
        boolean firstRowZero = false, firstColumnZero = false;

        for(int c=0; c<n; c++){
            if(matrix[0][c] == 0){
                firstRowZero = true;
                break;
            }
        }
        for(int r=0; r<m; r++){
            if(matrix[r][0] == 0){
                firstColumnZero = true;
                break;
            }
        }

        for(int r=1; r<m; r++){
            for(int c=1; c<n; c++){
                if(matrix[r][c] == 0){
                    matrix[r][0] = 0;
                    matrix[0][c] = 0;
                }
            }
        }

        for(int r=1; r<m; r++){
            for(int c=1; c<n; c++){
                if(matrix[r][0] == 0 || matrix[0][c] == 0){
                    matrix[r][c] = 0;
                }
            }
        }

        if(firstRowZero){
            for(int c=0; c<n; c++)  matrix[0][c] = 0;
        }
        if(firstColumnZero){
            for(int r=0; r<m; r++) matrix[r][0] = 0;
        }
    }
}
```
