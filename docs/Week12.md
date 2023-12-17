# Week 12

#### Connected Cells in a Grid
```java
import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

public class Solution {

    static int[][] grid;
    static boolean[][] visited;
    static int N, M;
    
    
    static int[] dx = {-1, 0, 1, 0, 1, 1, -1, -1}; 
    static int[] dy = {0, 1, 0, -1, 1, -1, 1, -1};

    static int count_connected(int row, int col) {
        if (row < 0 || row >= N || col < 0 || col >= M || grid[row][col] == 0 || visited[row][col]) return 0;
        visited[row][col] = true;
        int cnt = 1;
        for (int i = 0; i < 8; i++) {
            int newX = row + dx[i]; 
            int newY = col + dy[i];
            cnt += count_connected(newX, newY); 
        }
        return cnt; 
    }
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        N = scanner.nextInt();
        M = scanner.nextInt();
        grid = new int[N][M];
        visited = new boolean[N][M];
        for (int i = 0; i < N; ++i) {
            for (int j = 0; j < M; ++j) {
                grid[i][j] = scanner.nextInt();
                visited[i][j] = false;
            }
        }
        int max = 0;
        for (int i = 0; i < N; ++i) {
            for (int j = 0; j < M; ++j) {
                if (grid[i][j] == 0 || visited[i][j]) continue;       
                int cnt = count_connected(i, j);
                if (max < cnt) max = cnt;
            }
        }
        
        System.out.println(max);
        
    }
}
```