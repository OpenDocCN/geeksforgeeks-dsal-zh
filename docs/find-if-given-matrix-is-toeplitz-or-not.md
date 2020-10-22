# 判断给定的矩阵是否为 Toeplitz

> 原文： [https://www.geeksforgeeks.org/find-if-given-matrix-is-toeplitz-or-not/](https://www.geeksforgeeks.org/find-if-given-matrix-is-toeplitz-or-not/)

给定一个正方形矩阵，请确定它是否为 Toeplitz 矩阵。 Toeplitz（或对角常数）矩阵是这样的矩阵，其中从左到右的每个**对角线降序**是恒定的，即对角线上的所有元素都是相同的。

通常，对于每个单元格`mat[i][j]`和所有有效单元格 `mat[i + k][j + k]`或`mat[i-k][j-k]`，如果每个单元格`mat[i][j]`与`mat[i-1][j-1]`，`mat[i + 1][j]`，`mat[i-2][j-2]`，`mat[i + 2][j + 2]`，...相同，则任何`n×n`矩阵`mat[][]`都是 Toeplitz 矩阵。

**示例**：

```
Input: mat[N][N] = {{ 6, 7, 8},
                    { 4, 6, 7},
                    { 1, 4, 6}},
Output : True;
Values in all diagonals are same.

Input: mat[N][N] = {{ 6, 7, 8, 9 },
                    { 4, 6, 7, 8 },
                    { 1, 4, 6, 7 },
                    { 0, 1, 4, 6 },
                    { 2, 0, 1, 4 }};
Output : True;

Input: mat[N][N] = {{ 6, 3, 8},
                    { 4, 9, 7},
                    { 1, 4, 6}},
Output : False;
```



这个想法很简单。 对于矩阵中第一行和第一列（或最后一行和最后一列）的每个元素，我们检查从该元素开始的对角降序是否具有相同的值。 如果发现任何对角线的值不同，则返回`false`。

## C++ 

```cpp

// C++ program to check whether given matrix 
// is a Toeplitz matrix or not 
#include <iostream> 
using namespace std; 
#define N 5 
#define M 4 

// Function to check if all elements present in 
// descending diagonal starting from position 
// (i, j) in the matrix are all same or not 
bool checkDiagonal(int mat[N][M], int i, int j) 
{ 
    int res = mat[i][j]; 
    while (++i < N && ++j < M) 
    { 
        // mismatch found 
        if (mat[i][j] != res) 
            return false; 
    } 

    // we only reach here when all elements 
    // in given diagonal are same 
    return true; 
} 

// Function to check whether given matrix is a 
// Toeplitz matrix or not 
bool isToepliz(int mat[N][M]) 
{ 
    // do for each element in first row 
    for (int i = 0; i < M; i++) 
    { 
        // check descending diagonal starting from 
        // position (0, j) in the matrix 
        if (!checkDiagonal(mat, 0, i)) 
            return false; 
    } 

    // do for each element in first column 
    for (int i = 1; i < N; i++) 
    { 
        // check descending diagonal starting from 
        // position (i, 0) in the matrix 
        if (!checkDiagonal(mat, i, 0)) 
            return false; 
    } 

    // we only reach here when each descending 
    // diagonal from left to right is same 
    return true; 
} 

// Driver code 
int main() 
{ 
    int mat[N][M] = 
    { 
        { 6, 7, 8, 9 }, 
        { 4, 6, 7, 8 }, 
        { 1, 4, 6, 7 }, 
        { 0, 1, 4, 6 }, 
        { 2, 0, 1, 4 } 
    }; 

    if (isToepliz(mat)) 
        cout << "Matrix is a Toepliz "; 
    else
        cout << "Matrix is not a Toepliz "; 

    return 0; 
} 

```

## Java

```java

// Java program to check whether given matrix 
// is a Toeplitz matrix or not 
import java.io.*; 

class GFG  
{ 
    public static int N = 5; 
    public static int M = 4; 

    // Function to check if all elements present in 
    // descending diagonal starting from position 
    // (i, j) in the matrix are all same or not 
    static boolean checkDiagonal(int mat[][], int i, int j) 
    { 
        int res = mat[i][j]; 
        while (++i < N && ++j < M) 
        { 
            // mismatch found 
            if (mat[i][j] != res) 
                return false; 
        } 

        // we only reach here when all elements 
        // in given diagonal are same 
        return true; 
    } 

    // Function to check whether given matrix is a 
    // Toeplitz matrix or not 
    static boolean isToepliz(int mat[][]) 
    { 
        // do for each element in first row 
        for (int i = 0; i < M; i++) 
        { 
            // check descending diagonal starting from 
            // position (0, j) in the matrix 
            if (!checkDiagonal(mat, 0, i)) 
                return false; 
        } 

        // do for each element in first column 
        for (int i = 1; i < N; i++) 
        { 
            // check descending diagonal starting from 
            // position (i, 0) in the matrix 
            if (!checkDiagonal(mat, i, 0)) 
                return false; 
        } 

        // we only reach here when each descending 
        // diagonal from left to right is same 
        return true; 
    } 

    // driver program 
    public static void main (String[] args)  
    { 
        int mat[][] = { { 6, 7, 8, 9 }, 
                        { 4, 6, 7, 8 }, 
                        { 1, 4, 6, 7 }, 
                        { 0, 1, 4, 6 }, 
                        { 2, 0, 1, 4 } 
                      }; 

        if (isToepliz(mat)) 
            System.out.println("Matrix is a Toepliz "); 
        else
            System.out.println("Matrix is not a Toepliz "); 
    } 
} 

// This code is contributed by Pramod Kumar 

```

## Python3

```py

# Python3 program to check whether given  
# matrix is a Toeplitz matrix or not 
N = 5
M = 4

# Function to check if all elements present in 
# descending diagonal starting from position 
# (i, j) in the matrix are all same or not 
def checkDiagonal(mat, i, j): 
    res = mat[i][j] 
    i += 1
    j += 1

    while (i < N and j < M): 

        # mismatch found 
        if (mat[i][j] != res): 
            return False

        i += 1
        j += 1

    # we only reach here when all elements 
    # in given diagonal are same 
    return True

# Function to check whether given   
# matrix is a Toeplitz matrix or not 
def isToeplitz(mat): 

    # do for each element in first row 
    for j in range(M): 

        # check descending diagonal starting from 
        # position (0, j) in the matrix 
        if not(checkDiagonal(mat, 0, j)): 
            return False

    # do for each element in first column 
    for i in range(1, N):  

        # check descending diagonal starting  
        # from position (i, 0) in the matrix 
        if not(checkDiagonal(mat, i, 0)): 
            return False

    return True

# Driver Code  
if __name__ == "__main__": 

    mat = [[6, 7, 8, 9], 
          [4, 6, 7, 8], 
          [1, 4, 6, 7], 
          [0, 1, 4, 6], 
          [2, 0, 1, 4]] 

    if(isToeplitz(mat)): 
        print("Matrix is a Toeplitz") 
    else: 
        print("Matrix is not a Toeplitz") 

# This code is contributed by Jasmine K Grewal 

```

## C# 

```cs

// C# program to check whether given matrix 
// is a Toeplitz matrix or not 
using System; 

class GFG { 

    public static int N = 5; 
    public static int M = 4; 

    // Function to check if all elements present in 
    // descending diagonal starting from position 
    // (i, j) in the matrix are all same or not 
    static bool checkDiagonal(int[,] mat, int i, int j) 
    { 

        int res = mat[i,j]; 
        while (++i < N && ++j < M) 
        { 

            // mismatch found 
            if (mat[i,j] != res) 
                return false; 
        } 

        // we only reach here when all elements 
        // in given diagonal are same 
        return true; 
    } 

    // Function to check whether given matrix is a 
    // Toeplitz matrix or not 
    static bool isToepliz(int [,] mat) 
    { 

        // do for each element in first row 
        for (int i = 0; i < M; i++) 
        { 

            // check descending diagonal starting from 
            // position (0, j) in the matrix 
            if (!checkDiagonal(mat, 0, i)) 
                return false; 
        } 

        // do for each element in first column 
        for (int i = 1; i < N; i++) 
        { 

            // check descending diagonal starting from 
            // position (i, 0) in the matrix 
            if (!checkDiagonal(mat, i, 0)) 
                return false; 
        } 

        // we only reach here when each descending 
        // diagonal from left to right is same 
        return true; 
    } 

    // driver program 
    public static void Main ()  
    { 
        int [,] mat = { { 6, 7, 8, 9 }, 
                        { 4, 6, 7, 8 }, 
                        { 1, 4, 6, 7 }, 
                        { 0, 1, 4, 6 }, 
                        { 2, 0, 1, 4 } 
                    }; 

        if (isToepliz(mat)) 
            Console.WriteLine("Matrix is a Toepliz "); 
        else
            Console.WriteLine("Matrix is not a Toepliz "); 
    } 
} 

// This code is contributed by KRV. 

```

## PHP

```php

<?php 
// PHP program to check whether  
// given matrix is a Toeplitz  
// matrix or not 

// Function to check if all  
// elements present in descending  
// diagonal starting from position  
// (i, j) in the matrix are all  
// same or not 
function checkDiagonal($mat, $i, $j) 
{ 
    $N = 5; $M = 4; 
    $res = $mat[$i][$j]; 
    while (++$i < $N && ++$j < $M) 
    { 
        // mismatch found 
        if ($mat[$i][$j] != $res) 
            return false; 
    } 

    // we only reach here when  
    // all elements in given  
    // diagonal are same 
    return true; 
} 

// Function to check whether  
// given matrix is a 
// Toeplitz matrix or not 
function isToepliz($mat) 
{ 
    $N = 5; $M = 4; 
    // do for each element in first row 
    for ($i = 0; $i < $M; $i++) 
    { 
        // check descending diagonal  
        // starting from position  
        // (0, j) in the matrix 
        if (!checkDiagonal($mat, 0, $i)) 
            return false; 
    } 

    // do for each element  
    // in first column 
    for ($i = 1; $i < $N; $i++) 
    { 
        // check descending diagonal 
        // starting from position  
        // (i, 0) in the matrix 
        if (!checkDiagonal($mat, $i, 0)) 
            return false; 
    } 

    // we only reach here when  
    // each descending diagonal  
    // from left to right is same 
    return true; 
} 

// Driver code 
$mat = array(array( 6, 7, 8, 9 ), 
             array( 4, 6, 7, 8 ), 
             array( 1, 4, 6, 7 ), 
             array( 0, 1, 4, 6 ), 
             array( 2, 0, 1, 4 )); 

if (isToepliz($mat)) 
    echo "Matrix is a Toepliz "; 
else
    echo "Matrix is not a Toepliz "; 

// This code is contributed  
// by nitin mittal.  
?> 

```

**输出**：

```
Matrix is a Toepliz

```

该解决方案的**时间复杂度**为 `O(n^2)`，因为我们仅遍历矩阵中的每个元素一次。

**参考**： [https://en.wikipedia.org/wiki/Toeplitz_matrix](https://en.wikipedia.org/wiki/Toeplitz_matrix)

