# 矩阵元素的总和，其中每个元素是行和列的整数除法

> 原文： [https://www.geeksforgeeks.org/sum-matrix-element-element-integer-division-row-column/](https://www.geeksforgeeks.org/sum-matrix-element-element-integer-division-row-column/)

考虑一个`NXN`矩阵，其中每个元素都是行号除以列号（整数除法），即`mat[i][j] = floor((i + 1) / (j + 1))`其中`0 <= i < n`和`0 <= j < n`。 任务是找到所有矩阵元素的和。

**示例**：

```
Input  : N = 2
Output : 4
2 X 2 matrix with given constraint:
1 0
2 1
Sum of matrix element: 4

Input  : N = 3
Output : 9

```



**方法 1（暴力）**：

运行两个循环，一个循环用于行，另一个循环用于列，并找到`i / j`的整数部分，然后添加到答案中。

以下是此方法的实现：

## C++ 

```cpp

// C++ program to find sum of matrix element 
// where each element is integer division of 
// row and column. 
#include<bits/stdc++.h> 
using namespace std; 

// Return sum of matrix element where each element 
// is division of its corresponding row and column. 
int findSum(int n) 
{ 
    int ans = 0; 
    for (int i = 1; i <= n; i++)   // for rows 
        for (int j = 1; j <= n; j++) // for columns 
            ans += (i/j); 
    return ans; 
} 

// Driven Program 
int main() 
{ 
    int N = 2; 
    cout << findSum(N) << endl; 
    return 0; 
} 

```