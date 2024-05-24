```java
class Solution {
    public boolean exist(char[][] board, String word) {
        int n = board.length, m = board[0].length;
        boolean flg = false;
        for(int i = 0; i < n; ++i){
            for(int j = 0; j < m; ++j){
                if(board[i][j] == word.charAt(0)){
                    int[][] visited = new int[n][m];
                    flg = bfs(board, word, i, j, visited, 0) || flg;
                    if(flg == true) return flg;
                }
            }
        }
        return flg;
    }

    private boolean bfs(char[][] board, String word, int x, int y, int[][] visited, int index){
        if(index == word.length()) return true;
        if(x < 0 || y < 0 || x >= board.length || y >= board[0].length) return false;
        if(board[x][y] != word.charAt(index) || visited[x][y] == 1) return false;
        visited[x][y] = 1;
        return bfs(board, word, x - 1, y, visited, index + 1) || bfs(board, word, x + 1, y, visited, index + 1) || bfs(board, word, x, y + 1, visited, index + 1) || bfs(board, word, x, y - 1, visited, index + 1);
    }
}
```

