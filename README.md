class Solution {
    static int check = 0;
    public boolean isValid(char[][] board, int r, int c, char num) {
         // check row
        for(int j = 0; j < 9; j++) {
            if(board[r][j]==num) return false;
        }   
        // check col
        for(int i = 0; i < 9; i++) {
            if(board[i][c]==num) return false;
        }        
        // check grid 
        int sRow = r/3*3;
        int sCol = c/3*3;
        for(int i = sRow; i < sRow+3; i++) {
            for(int j = sCol; j < sCol+3; j++) {
                if(board[i][j]==num) return false;
            }
        }            
        return true;
    }
    public void solve(char[][] board, int r, int c) {
        if(r == 9) {
            check = 1;
            return;
        } 
        else if(board[r][c] != '.') { //call
            if(c != 8) solve(board, r, c+1);
            else solve(board, r+1, 0);
        }
         else {// board[row][col]!='.'
            for(char ch = '1'; ch <= '9'; ch++) {
                if(isValid(board,r,c,ch)) {
                    board[r][c]=ch;
                    if(c!=8) solve(board,r,c+1);
                    else solve(board,r+1,0);
                    if(check == 1) return;
                    board[r][c] = '.';// backtracking
                }
            }
        }
    }
    public void solveSudoku(char[][] board) {
        solve(board,0,0);
        check = 0;
    }
}  
