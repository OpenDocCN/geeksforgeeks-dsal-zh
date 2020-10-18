# 程序用矩阵的下对角元素交换上对角元素。

> 原文： [https://www.geeksforgeeks.org/program-swap-upper-diagonal-elements-lower-diagonal-elements-matrix/](https://www.geeksforgeeks.org/program-swap-upper-diagonal-elements-lower-diagonal-elements-matrix/)

给定一个正方形矩阵，将矩阵的上对角线元素与矩阵的下对角线元素交换。

**示例**：

```
Input:   2  3  5  6
         4  5  7  9
         8  6  4  9
         1  3  5  6

Output:  2  4  8  1
         3  5  6  3
         5  7  4  5
         6  9  9  6

Input:   1  2  3 
         4  5  6
         7  8  9

Output:  1  4  7
         2  5  8
         3  6  9

```



以下是上述想法的实现：

## C++ 

```cpp

// CPP Program to implement matrix 
// for swapping the upper diagonal 
// elements with lower diagonal  
// elements of matrix. 
#include <bits/stdc++.h> 
#define n 4 
using namespace std; 

// Function to swap the diagonal  
// elements in a matrix. 
void swapUpperToLower(int arr[n][n]) 
{ 
    // Loop for swap the elements of matrix. 
    for (int i = 0; i < n; i++) { 
        for (int j = i + 1; j < n; j++) { 
            int temp = arr[i][j]; 
            arr[i][j] = arr[j][i]; 
            arr[j][i] = temp; 
        } 
    } 

    // Loop for print the matrix elements. 
    for (int i = 0; i < n; i++) { 
        for (int j = 0; j < n; j++) 
            cout << arr[i][j] << " "; 
        cout << endl; 
    } 
} 

// Driver function to run the program 
int main() 
{ 
    int arr[n][n] = { { 2, 3, 5, 6 }, 
                    { 4, 5, 7, 9 }, 
                    { 8, 6, 4, 9 }, 
                    { 1, 3, 5, 6 } }; 

    // Function call 
    swapUpperToLower(arr); 
    return 0; 
} 

} 

```