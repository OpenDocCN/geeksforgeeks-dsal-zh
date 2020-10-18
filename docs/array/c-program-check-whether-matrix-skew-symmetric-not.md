# C 程序检查矩阵是否倾斜对称

> 原文： [https://www.geeksforgeeks.org/c-program-check-whether-matrix-skew-symmetric-not/](https://www.geeksforgeeks.org/c-program-check-whether-matrix-skew-symmetric-not/)

倾斜对称矩阵或反对称矩阵是方阵，其转置与原始矩阵的转置相反。 如果矩阵的第`i`行和第`j`列中的条目为`a[i][j]`，即如果`A = (a[i][j])`， 倾斜对称条件为`-A = -a[j][i]`。

**示例**：

```
Input : matrix:     0   5  -4          
                   -5   0   1                            
                    4  -1   0                            
 Output: 
Transpose matrix:   0  -5   4
                    5   0   1
                   -4   1   0
Skew Symmetric matrix

```

**步骤**：

1.  找到输入矩阵的转置。

2.  如果输入矩阵等于其转置矩阵的负值，则该矩阵为“斜对称”。



## C++ 

```cpp

// C program to check whether given matrix 
// is skew-symmetric or not 
#include <stdio.h> 
#include <stdlib.h> 

#define ROW 3 
#define COL 3 

// Utility function to create transpose matrix 
void transpose(int transpose_matrix[ROW][COL], 
                         int matrix[ROW][COL]) 
{ 
   for (int i = 0; i < ROW; i++) 
      for (int j = 0; j < COL; j++) 
         transpose_matrix[j][i] = matrix[i][j]; 
} 

// Utility function to check skew - symmetric 
// matrix condition 
bool check(int transpose_matrix[ROW][COL], 
                    int matrix[ROW][COL]) 
{ 
    for (int i = 0; i < ROW; i++) 
        for (int j = 0; j < COL; j++) 
            if (matrix[i][j] != -transpose_matrix[i][j]) 
                return false; 
    return true; 
} 

// Utility function to print a matrix 
void printMatrix(int matrix[ROW][COL]) 
{ 
    for (int i = 0; i < ROW; i++) 
    { 
       for (int j = 0; j < COL; j++) 
            printf("%d ", matrix[i][j]); 
       printf("\n"); 
    } 
} 

// Driver program to test above functions 
int main() 
{ 
    int matrix[ROW][COL] = { 
                            {0, 5, -4}, 
                            {-5, 0, 1}, 
                            {4, -1, 0}, 
                           }; 

    int transpose_matrix[ROW][COL]; 

    // Function create transpose matrix 
    transpose(transpose_matrix, matrix); 

    printf ("Transpose matrix: \n"); 
    printMatrix(transpose_matrix); 

    // Check whether matrix is skew-symmetric or not 
    if (check(transpose_matrix, matrix)) 
       printf("Skew Symmetric Matrix"); 
    else
       printf("Not Skew Symmetric Matrix"); 

    return 0; 
} 

```

## Java

```java

// java program to check 
// whether given matrix 
// is skew-symmetric or not 
import java.io.*; 

class GFG { 

static int ROW =3; 
static int COL =3; 

// Utility function to create transpose matrix 
 static void transpose(int transpose_matrix[][], 
                        int matrix[][]) 
{ 
for (int i = 0; i < ROW; i++) 
    for (int j = 0; j < COL; j++) 
        transpose_matrix[j][i] = matrix[i][j]; 
} 

// Utility function to check skew - symmetric 
// matrix condition 
 static boolean check(int transpose_matrix[][], 
                    int matrix[][]) 
{ 
    for (int i = 0; i < ROW; i++) 
        for (int j = 0; j < COL; j++) 
            if (matrix[i][j] != -transpose_matrix[i][j]) 
                return false; 
    return true; 
} 

// Utility function to print a matrix 
 static void printMatrix(int matrix[][]) 
{ 
    for (int i = 0; i < ROW; i++) 
    { 
    for (int j = 0; j < COL; j++) 
            System.out.print(matrix[i][j] + " "); 
    System.out.println(); 
    } 
} 

// Driver program to test above functions 
public static void main (String[] args) { 
        int matrix[][] = { 
                            {0, 5, -4}, 
                            {-5, 0, 1}, 
                            {4, -1, 0}, 
                        }; 

    int transpose_matrix[][] = new int[ROW][COL]; 

    // Function create transpose matrix 
    transpose(transpose_matrix, matrix); 

    System.out.println ("Transpose matrix: "); 
    printMatrix(transpose_matrix); 

    // Check whether matrix is skew-symmetric or not 
    if (check(transpose_matrix, matrix)) 
    System.out.println("Skew Symmetric Matrix"); 
    else
    System.out.println("Not Skew Symmetric Matrix"); 

    } 
} 

// This code is contributed by vt_m. 

```

## Python3

```py

# Python 3 program to check 
# whether given matrix 
# is skew-symmetric or not 
ROW=3
COL=3

# Utility function to 
# create transpose matrix 
def transpose(transpose_matrix,matrix): 
    for i in range (ROW): 
        for j in range(COL): 
            transpose_matrix[j][i] = matrix[i][j] 

# Utility function to 
# check skew - symmetric 
# matrix condition 
def check(transpose_matrix,matrix): 
    for i in range(ROW): 
        for j in range(COL): 
            if (matrix[i][j] != -transpose_matrix[i][j]): 
                return False
    return True

# Utility function to print a matrix 
def printMatrix(matrix): 
    for i in range (ROW): 
        for j in range(COL): 
            print(matrix[i][j]," ",end="") 
        print() 

# Driver program to test above functions 
matrix= [ 
            [0, 5, -4], 
            [-5, 0, 1], 
            [4, -1, 0], 
        ] 
transpose_matrix=[[0 for i in range(3)] for j in range(3)] 

# Function create transpose matrix 
transpose(transpose_matrix, matrix) 
print("Transpose matrix:") 
printMatrix(transpose_matrix) 

# Check whether matrix is 
# skew-symmetric or not 
if (check(transpose_matrix, matrix)): 
    print("Skew Symmetric Matrix") 
else: 
    print("Not Skew Symmetric Matrix") 

# This code is contributed 
# by Azkia Anam. 

```

## C# 

```cs

// C# program to check 
// whether given matrix 
// is skew-symmetric or not 
using System; 

class GFG  
{ 
static int ROW =3; 
static int COL =3; 

// Utility function to 
// create transpose matrix 
static void transpose(int [,]transpose_matrix, 
                      int [,]matrix) 
{ 
for (int i = 0; i < ROW; i++) 
    for (int j = 0; j < COL; j++) 
        transpose_matrix[j,i] = matrix[i,j]; 
} 

// Utility function to check  
// skew - symmetric matrix  
// condition 
static bool check(int [,]transpose_matrix, 
                  int [,]matrix) 
{ 
    for (int i = 0; i < ROW; i++) 
        for (int j = 0; j < COL; j++) 
            if (matrix[i, j] !=  
                -transpose_matrix[i, j]) 
                return false; 
    return true; 
} 

// Utility function 
// to print a matrix 
static void printMatrix(int [,]matrix) 
{ 
    for (int i = 0; i < ROW; i++) 
    { 
    for (int j = 0; j < COL; j++) 
            Console.Write(matrix[i, j] +  
                                   " "); 
    Console.WriteLine(); 
    } 
} 

// Driver Code 
public static void Main ()  
{ 
    int [,]matrix = {{0, 5, -4}, 
                     {-5, 0, 1}, 
                     {4, -1, 0},}; 

    int [,]transpose_matrix = new int[ROW, COL]; 

    // Function create transpose matrix 
    transpose(transpose_matrix, matrix); 

    Console.WriteLine("Transpose matrix: "); 
    printMatrix(transpose_matrix); 

    // Check whether matrix is 
    // skew-symmetric or not 
    if (check(transpose_matrix, matrix)) 
    Console.WriteLine("Skew Symmetric Matrix"); 
    else
    Console.WriteLine("Not Skew Symmetric Matrix"); 
    } 
} 

// This code is contributed by anuj_67\. 

```

**输出**：

```
Transpose matrix: 
0 -5 4 
5 0 -1 
-4 1 0 
Skew Symmetric Matrix

```

 **参考**： [维基百科](https://en.wikipedia.org/wiki/Skew-symmetric_matrix)

