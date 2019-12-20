#[leetcode][알고리즘][array]289 - game_of_life (medium)
### (https://leetcode.com/problems/game-of-life/)



![img34](/image/img34.png)


![img35](/image/img35.png)


![img36](/image/img36.png)
 

 


```
class Solution {
public:
    int countNeighbors(int x, int y, int row, int col, vector<vector<int> >& board){
        int dx[8] = {-1, -1, -1, 0, 1, 1, 1, 0};
        int dy[8] = {-1, 0, 1, 1, 1, 0, -1, -1};
        
        int nx, ny;
        int cnt = 0;
        for(int d=0; d<8; d++){
            nx = x + dx[d];
            ny = y + dy[d];
            if( 0<=nx && nx<row && 0<=ny && ny<col && board[nx][ny]>=1) cnt++;
        }
        
        return cnt;
    }
    
    void gameOfLife(vector<vector<int>>& board) {
        
        int m = board.size();
        int n = board[0].size();
        
        int cntOfNeighbors;
        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                cntOfNeighbors = countNeighbors(i, j, m, n, board);
                if( board[i][j]==0 && cntOfNeighbors==3 ) board[i][j] = -1; // 0 -> 1로 바껴야하는 경우 
                else if( board[i][j]==1 && (cntOfNeighbors<2 || cntOfNeighbors>3) ) board[i][j] = 2; //1 -> 0으로 바껴야하는 경우
                // 나머지는 그대로 두기 
            }
        }
        
        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                cout<<board[i][j]<<" ";
                if(board[i][j]==-1) board[i][j] = 1;
                else if(board[i][j]==2) board[i][j] = 0;
                
            }
            cout<<endl;
        } 
    }
};
```

* 이중배열 문제에서, Space complexity를 O(mn)에서 O(1)로 줄일 수 있다. 
