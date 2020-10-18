# 给定矩阵`O`和`X`，找到被`X`包围的最大子正方形

> 原文： [https://www.geeksforgeeks.org/given-matrix-o-x-find-largest-subsquare-surrounded-x/](https://www.geeksforgeeks.org/given-matrix-o-x-find-largest-subsquare-surrounded-x/)

给定一个矩阵，其中每个元素均为`O`或`X`，请找到被`X`包围的最大子正方形。

在下面的文章中，假定给定矩阵也是方阵。 下面给出的代码可以很容易地扩展到矩形矩阵。

**示例**：

```
Input: mat[N][N] = { {'X', 'O', 'X', 'X', 'X'},
                     {'X', 'X', 'X', 'X', 'X'},
                     {'X', 'X', 'O', 'X', 'O'},
                     {'X', 'X', 'X', 'X', 'X'},
                     {'X', 'X', 'X', 'O', 'O'},
                    };
Output: 3
The square submatrix starting at (1, 1) is the largest
submatrix surrounded by 'X'

Input: mat[M][N] = { {'X', 'O', 'X', 'X', 'X', 'X'},
                     {'X', 'O', 'X', 'X', 'O', 'X'},
                     {'X', 'X', 'X', 'O', 'O', 'X'},
                     {'X', 'X', 'X', 'X', 'X', 'X'},
                     {'X', 'X', 'X', 'O', 'X', 'O'},
                    };
Output: 4
The square submatrix starting at (0, 2) is the largest
submatrix surrounded by 'X'

```



一种**简单解决方案**是考虑每个正方形子矩阵，并检查是否所有角边都填充有`X`。 该解决方案的时间复杂度为`O(N ^ 4)`。

我们可以在`O(N ^ 3)`时间中使用额外的空间来解决此问题。 这个想法是创建两个辅助数组`hor[N][N]`和`ver[N][N]`。 存储在`hor[i][j]`中的值是直到`mat[][]`中的`mat[i][j]`为止的水平连续`X`字符数。 同样，存储在`ver[i][j]`中的值是直到`mat[][]`中的`mat[i][j]`为止的垂直连续`X`字符数。 以下是一个示例。

```

mat[6][6] =  X  O  X  X  X  X
             X  O  X  X  O  X
             X  X  X  O  O  X
             O  X  X  X  X  X
             X  X  X  O  X  O
             O  O  X  O  O  O

hor[6][6] = 1  0  1  2  3  4
            1  0  1  2  0  1
            1  2  3  0  0  1
            0  1  2  3  4  5
            1  2  3  0  1  0
            0  0  1  0  0  0

ver[6][6] = 1  0  1  1  1  1
            2  0  2  2  0  2
            3  1  3  0  0  3
            0  2  4  1  1  4
            1  3  5  0  2  0
            0  0  6  0  0  0
```

一旦我们在`hor[][]`和`ver[][]`中填充了值，就从矩阵的最右下角开始，并逐行地移到最左上角。 对于每个访问的入口`mat[i][j]`，我们比较`hor[i][j]`和`ver[i][j]`的值，并选择两个中较小的一个作为正方形。 假设其中两个较小的为`small`。 选择两个较小的值后，我们分别检查`ver[][]`和`hor[][]`的左边缘和上边缘。 如果他们有相同的条目，那么我们找到了一个子正方形。 否则，我们尝试使用`small-1`。

以下是上述想法的实现。

## C++ 

```cpp

// A C++ program to find  the largest subsquare 
// surrounded by 'X' in a given matrix of 'O' and 'X' 
#include<iostream> 
using namespace std; 

// Size of given matrix is N X N 
#define N 6 

// A utility function to find minimum of two numbers 
int getMin(int x, int y) { return (x<y)? x: y; } 

// Returns size of maximum size subsquare matrix 
// surrounded by 'X' 
int findSubSquare(int mat[][N]) 
{ 
    int max = 0; // Initialize result 

    // Initialize the left-top value in hor[][] and ver[][] 
    int hor[N][N], ver[N][N]; 
    hor[0][0] = ver[0][0] = (mat[0][0] == 'X'); 

    // Fill values in hor[][] and ver[][] 
    for (int i=0; i<N; i++) 
    { 
        for (int j=0; j<N; j++) 
        { 
            if (mat[i][j] == 'O') 
                ver[i][j] = hor[i][j] = 0; 
            else
            { 
                hor[i][j] = (j==0)? 1: hor[i][j-1] + 1; 
                ver[i][j] = (i==0)? 1: ver[i-1][j] + 1; 
            } 
        } 
    } 

    // Start from the rightmost-bottommost corner element and find 
    // the largest ssubsquare with the help of hor[][] and ver[][] 
    for (int i = N-1; i>=1; i--) 
    { 
        for (int j = N-1; j>=1; j--) 
        { 
            // Find smaller of values in hor[][] and ver[][] 
            // A Square can only be made by taking smaller 
            // value 
            int small = getMin(hor[i][j], ver[i][j]); 

            // At this point, we are sure that there is a right 
            // vertical line and bottom horizontal line of length 
            // at least 'small'. 

            // We found a bigger square if following conditions 
            // are met: 
            // 1)If side of square is greater than max. 
            // 2)There is a left vertical line of length >= 'small' 
            // 3)There is a top horizontal line of length >= 'small' 
            while (small > max) 
            { 
                if (ver[i][j-small+1] >= small && 
                    hor[i-small+1][j] >= small) 
                { 
                    max = small; 
                } 
                small--; 
            } 
        } 
    } 
    return max; 
} 

// Driver program to test above function 
int main() 
{ 
    int mat[][N] =  {{'X', 'O', 'X', 'X', 'X', 'X'}, 
                     {'X', 'O', 'X', 'X', 'O', 'X'}, 
                     {'X', 'X', 'X', 'O', 'O', 'X'}, 
                     {'O', 'X', 'X', 'X', 'X', 'X'}, 
                     {'X', 'X', 'X', 'O', 'X', 'O'}, 
                     {'O', 'O', 'X', 'O', 'O', 'O'}, 
                    }; 
    cout << findSubSquare(mat); 
    return 0; 
} 

```