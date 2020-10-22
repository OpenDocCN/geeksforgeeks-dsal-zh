# 以各种方式对矩阵排序

> 原文： [https://www.geeksforgeeks.org/sort-matrix-way-increasing-order/](https://www.geeksforgeeks.org/sort-matrix-way-increasing-order/)

给定具有不同元素的`N * N`阶方阵，任务是对给定矩阵进行排序，使其行，列和对角线（对角线和反对角线）的顺序都递增。

例子：

```
Input : arr[3][3] = {1, 4, 2,
                     3, 5, 6,
                     9, 7, 8}
Output :{1, 2, 3,
         4, 5, 6,
         7, 8, 9}

Input : arr[2][2] = {0, 4,
                     5, 2}                    
Output :{0, 2,
         4, 5}

```



以行，列和主对角线升序排列的方式对任何矩阵进行排序很容易。 如果我们根据行的主要顺序依次考虑矩阵元素并对其进行排序，则可以得到所需的结果。

```
Example: arr[2][2] : {1, 2
                      3, 4}
Rows in increasing order:  {1,2} and {3,4}
Columns in increasing order:  {1,3} and {2,4}
Diagonal in increasing order:  {1,4}
Anti-diagonal in increasing order:  {2,3}

```

```

// C++ program to sort matrix in all-way 
#include<bits/stdc++.h> 
using namespace std; 
#define N 3 

// Sorts a matrix in increasing order 
void sortAllWay(int arr[][N]) 
{ 
    // Consider matrix elements (in row major 
    // order) and sort the sequence. 
    int *ptr = (int *)arr; 
    sort(ptr, ptr+N*N); 
} 

// driver program 
int main() 
{ 
    int arr[N][N] = {1, 0, 3, 
                     2, 5, 6, 
                     9, 4, 8}; 
    sortAllWay(arr); 

    // print resultant matrix 
    for (int i=0; i<N; i++) 
    { 
        for (int j=0; j<N; j++) 
            cout << arr[i][j] << " "; 
        cout <<"\n"; 
    } 

    return 0; 
} 

```

输出：

```
0 1 2 
3 4 5 
6 8 9

```

时间复杂度：`O(N * N log N)`。

辅助空间：`O(N * N)`。



