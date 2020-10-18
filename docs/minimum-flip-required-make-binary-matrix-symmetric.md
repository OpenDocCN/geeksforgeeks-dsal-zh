# 使二进制矩阵对称所需的最小翻转

> 原文： [https://www.geeksforgeeks.org/minimum-flip-required-make-binary-matrix-symmetric/](https://www.geeksforgeeks.org/minimum-flip-required-make-binary-matrix-symmetric/)

给定大小为`N X N`的二进制矩阵，由 1 和 0 组成。 任务是找到使矩阵沿[主对角线](https://en.wikipedia.org/wiki/Main_diagonal)对称所需的最小翻转。

**示例**：

```
Input : mat[][] = { { 0, 0, 1 },
                    { 1, 1, 1 },
                    { 1, 0, 0 } };
Output : 2
Value of mat[1][0] is not equal to mat[0][1].
Value of mat[2][1] is not equal to mat[1][2].
So, two flip are required.

Input : mat[][] = { { 1, 1, 1, 1, 0 },
                    { 0, 1, 0, 1, 1 },
                    { 1, 0, 0, 0, 1 },
                    { 0, 1, 0, 1, 0 },
                    { 0, 1, 0, 0, 1 } };                  
Output : 3

```



**方法 1（简单）**：

这个想法是找到矩阵的转置并找到使转置和原始矩阵相等所需的最小翻转次数。 要找到最小翻转，请找到原始矩阵和转置矩阵不相同的位置数，例如`x`。 因此，我们的答案将是`x / 2`。

以下是此方法的实现：

## C++ 

```cpp

// CPP Program to find minimum flip required to make 
// Binary Matrix symmetric along main diagonal 
#include <bits/stdc++.h> 
#define N 3 
using namespace std; 

// Return the minimum flip required to make 
// Binary Matrix symmetric along main diagonal. 
int minimumflip(int mat[][N], int n) 
{ 
    int transpose[n][n]; 

    // finding the transpose of the matrix 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < n; j++) 
            transpose[i][j] = mat[j][i]; 

    // Finding the number of position where 
    // element are not same. 
    int flip = 0; 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < n; j++) 
            if (transpose[i][j] != mat[i][j]) 
                flip++; 

    return flip / 2; 
} 

// Driver Program 
int main() 
{ 
    int n = 3; 
    int mat[N][N] = { 
        { 0, 0, 1 }, 
        { 1, 1, 1 }, 
        { 1, 0, 0 } 
    }; 
    cout << minimumflip(mat, n) << endl; 
    return 0; 
} 

```