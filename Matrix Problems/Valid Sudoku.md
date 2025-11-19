Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:  
  
Each row must contain the digits 1-9 without repetition.  
Each column must contain the digits 1-9 without repetition.  
Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.  
Note:  
A Sudoku board (partially filled) could be valid but is not necessarily solvable.  
Only the filled cells need to be validated according to the mentioned rules.  
  
Example 1:  
![Valid Sudoku](Images/sudoku.webp)  
Input: board =   
[["5","3",".",".","7",".",".",".","."]  
,["6",".",".","1","9","5",".",".","."]  
,[".","9","8",".",".",".",".","6","."]  
,["8",".",".",".","6",".",".",".","3"]  
,["4",".",".","8",".","3",".",".","1"]  
,["7",".",".",".","2",".",".",".","6"]  
,[".","6",".",".",".",".","2","8","."]  
,[".",".",".","4","1","9",".",".","5"]  
,[".",".",".",".","8",".",".","7","9"]]  
Output: true  
  
Example 2:  
Input: board =   
[["8","3",".",".","7",".",".",".","."]  
,["6",".",".","1","9","5",".",".","."]  
,[".","9","8",".",".",".",".","6","."]  
,["8",".",".",".","6",".",".",".","3"]  
,["4",".",".","8",".","3",".",".","1"]  
,["7",".",".",".","2",".",".",".","6"]  
,[".","6",".",".",".",".","2","8","."]  
,[".",".",".","4","1","9",".",".","5"]  
,[".",".",".",".","8",".",".","7","9"]]  
Output: false  
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.  
  
Constraints:  
board.length == 9  
board[i].length == 9  
board[i][j] is a digit 1-9 or '.'.  
  
Code: Java  
  
```
class Solution {
    public boolean isValidSudoku(char[][] board) {
        int[] rows = new int[9];
        int[] cols = new int[9];
        int[] boxes = new int[9];

        for(int r=0; r<9; r++){
            for(int c=0; c<9; c++){
                char ch = board[r][c];
                if(ch == '.') continue;
                int digit = ch - '0';
                int mask = 1 << (digit - 1);

                if((rows[r] & mask) != 0) return false;
                rows[r] |= mask;

                if((cols[c] & mask) != 0) return false;
                cols[c] |= mask;

                int boxIndex = (r/3)*3 + (c/3);
                if((boxes[boxIndex] & mask) != 0) return false;
                boxes[boxIndex] |= mask;
            }
        }
        return true;
    }
}
```  
Time Complexity: O(1), Sudoku grid size is always fixed (9×9). The number of operations does not grow with input size.  
Space Complexity: O(1), Uses fixed-size 27 integers (rows, cols, boxes)  
  
Explanation:  
mask = 1 << (d - 1)   
->   Left shift the bit by (d-1), if digit = 5   ->   mask = 1 << (5-1) = 1 << 4   ->   mask = 00010000 (binary)  
->   if digit = 7   ->   mask = 1 << (7-1) = 1 << 6 = 64    ->    mask = 01000000  
  
(rows[r] & mask) != 0   ->  rows[r] = 000010000  &&  mask = 01000000  =  000000000 (zero!)  
  
rows[r] |= mask;   ->  00010100 (previous)  ||  01000000 (digit 7)  =  01010100  
(r/3)*3 + (c/3)  ->  Position (4,8)  ->   r = 4 → r/3 = 1, c = 8 → c/3 = 2  ->  boxIndex = 1*3 + 2 = 5  
  
Box Indexing:  
0 1 2  
3 4 5  
6 7 8  
