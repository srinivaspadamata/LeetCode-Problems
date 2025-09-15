You are given an m x n grid where each cell can have one of three values:  
0 representing an empty cell,  
1 representing a fresh orange, or  
2 representing a rotten orange.  
Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten.  
  
Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return -1.  
  
Example 1:  
![rotting oranges](Images/rottenoranges.png)  
Input: grid = [[2,1,1],[1,1,0],[0,1,1]]  
Output: 4  
  
Example 2:  
Input: grid = [[2,1,1],[0,1,1],[1,0,1]]  
Output: -1  
Explanation: The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.  
  
Example 3:  
Input: grid = [[0,2]]  
Output: 0  
Explanation: Since there are already no fresh oranges at minute 0, the answer is just 0.  
  
Constraints:  
m == grid.length  
n == grid[i].length  
1 <= m, n <= 10  
grid[i][j] is 0, 1, or 2.  

Code: Java  
  
```
class Solution {
    public int orangesRotting(int[][] grid) {
        int[][] dir = {{1,0},{0,1},{-1,0},{0,-1}};
        int n = grid.length, m = grid[0].length;
        Queue<int[]> queue = new LinkedList<>();
        int minute = -1, fresh = 0;

        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(grid[i][j] == 2) queue.add(new int[]{i,j});
                else if(grid[i][j] == 1) fresh++;
            }
        }
        
        if(fresh == 0) return 0;

        while(!queue.isEmpty()){
            int size = queue.size();
            minute++;
            for(int i=0; i<size; i++){
                int[] curr = queue.poll();
                int r = curr[0], c = curr[1];
                for(int[] d: dir){
                    int  nr = d[0] + r, nc = d[1] + c;
                    if(nr >= 0 && nr < n && nc >= 0 && nc < m && grid[nr][nc] == 1){
                        grid[nr][nc] = 2;
                        fresh--;
                        queue.add(new int[]{nr,nc});
                    }
                }
            }
        }
        return fresh == 0 ? minute : -1;
    }
}
```
Time Complexity: O(n * m), n = number of rows, m = number of columns.  
Space Complexity: O(n * m), Queue: in the worst case, all oranges could be rotten at the same time → O(m * n)  
