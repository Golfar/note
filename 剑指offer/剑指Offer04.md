# 二维数组中的查找

[240. 搜索二维矩阵 II - 力扣（LeetCode）](https://leetcode.cn/problems/search-a-2d-matrix-ii/description/)

编写一个高效的算法来搜索 `m x n` 矩阵 `matrix` 中的一个目标值 `target` 。该矩阵具有以下特性：

- 每行的元素从左到右升序排列。
- 每列的元素从上到下升序排列。

**提示：**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= n, m <= 300`
- `-109 <= matrix[i][j] <= 109`
- 每行的所有元素从左到右升序排列
- 每列的所有元素从上到下升序排列
- `-109 <= target <= 109`

## 方法一：直接遍历

## 方法二：按行二分

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        for(int[] row : matrix){
            if(erfen(row, target)) return true;
        }
        return false;
    }
    public boolean erfen(int[] row, int target){
        int l = 0, r = row.length - 1;
        while(l <= r){
            int mid = (l + r) >> 1;
            if(row[mid] == target) return true;
            if(row[mid] > target) r = mid - 1;
            else l = mid + 1;
        }
        return false;
    }
}
```

## 方法三：z字搜索

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int n = matrix.length, m = matrix[0].length;
        int x = 0, y = m - 1;
        while(x < n && y >= 0){
            if(matrix[x][y] == target) return true;
            if(matrix[x][y] > target) --y;
            else ++x;
        }
        return false;
    }
}
```

从右上角开始搜索