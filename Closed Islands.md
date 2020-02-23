Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:

Input:
11110
11010
11000
00000

Output: 1
Example 2:

Input:
11000
11000
00100
00011

Output: 3


```java
private static final int[][] DIRS = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
public int numIslands(char[][] grid) {
	int r = grid.length;
	if (r == 0)
		return 0;
	int c = grid[0].length;
	int count = 0;
	for (int i = 0; i < r; i++) 
		for (int j = 0; j < c; j++) 
			if (grid[i][j] == '1') {
				dfs(grid, i, j, r, c);
				count++;
			}
	return count;
}

private void dfs(char[][] grid, int i, int j, int r, int c) {
	if (i == -1 || i == r || j == -1 || j == c || grid[i][j] == '0')
		return;
	grid[i][j] = '0';
	for (int d = 0; d < DIRS.length; d++)
		dfs(grid, i + DIRS[d][0], j + DIRS[d][1], r, c);
}

```
