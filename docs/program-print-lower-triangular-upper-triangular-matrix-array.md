# 打印数组的下三角和上三角矩阵的程序

> 原文： [https://www.geeksforgeeks.org/program-print-lower-triangular-upper-triangular-matrix-array/](https://www.geeksforgeeks.org/program-print-lower-triangular-upper-triangular-matrix-array/)

先决条件：[C/C++ 中的多维数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)

给定一个二维数组，编写一个程序以打印下三角矩阵和上三角矩阵。

*   下三角矩阵是一个矩阵，其中包含在原理对角线以下的元素（包括原理对角线元素），其余元素为 0。

*   上三角矩阵是一个矩阵，其中包含在原则对角线上的元素（包括原则对角元素），其余元素为 0。

**下三角**：

![{\displaystyle \begin{bmatrix} A_{00} & 0 & 0 & ... & 0\\  A_{10} & A_{11} & 0 & ... & 0\\  A_{20} & A_{21} & A_{22} & ... & 0\\  . & . & . & . & .\\  . &  &  &  & \\  . &  &  &  & \\  . &  &  &  & \\  . &  &  &  & \\  . &  &  &  & \\  A_{row0} & A_{row1} & A_{row2} & ... & A_{rowcol} \end{bmatrix}}](img/1d15ce203b3074caefa5c3ddd1b18a19.png "Rendered by QuickLaTeX.com")

**上矩形**：

![{\displaystyle \begin{bmatrix} A_{00} & A_{01} & A_{02} & ... & A_{0col}\\  0 & A_{11} & A_{22} & ... & A_{1col}\\  0 & 0 & A_{22} & ... & A_{2col}\\  . & . & . & . & .\\  . &  &  &  & \\  . &  &  &  & \\  . &  &  &  & \\  . &  &  &  & \\  . &  &  &  & \\  0 & 0 & 0 & ... & A_{rowcol} \end{bmatrix}}](img/a8f3a1c976f77ddb9a937ea583f911a9.png "Rendered by QuickLaTeX.com")

**示例**：

```
Input : matrix[3][3] = {1 2 3
                       4 5 6
                       7 8 9}
Output :
Lower : 1 0 0        Upper : 1 2 3
        4 5 0                0 5 6
        7 8 9                0 0 9

Input : matrix[3][3] = {7 8 9
                        3 2 1
                        6 5 4}
Output :
Lower : 7 0 0       Upper : 7 8 9
        3 2 0               0 2 1
        6 5 4               0 0 4

```

**步骤**：

1.  对于下三角矩阵，我们分别检查索引位置`i`和`j`，即行和列。 如果列位置大于行位置，我们只需将该位置设为 0。

2.  对于上三角矩阵，我们分别检查索引位置`i`和`j`，即行和列。 如果列位置小于行位置，我们只需将该位置设为 0。



## C++ 

```cpp

// C++ program to print Lower  
// triangular and Upper triangular 
// matrix of an array 
#include<iostream> 

using namespace std; 

// Function to form  
// lower triangular matrix 
void lower(int matrix[3][3], int row, int col) 
{ 
    int i, j; 
    for (i = 0; i < row; i++) 
    { 
        for (j = 0; j < col; j++) 
        { 
            if (i < j) 
            { 
                cout << "0" << " "; 
            } 
            else
            cout << matrix[i][j] << " "; 
        } 
        cout << endl; 
    } 
} 

// Function to form upper triangular marix 
void upper(int matrix[3][3], int row, int col) 
{ 
    int i, j; 

    for (i = 0; i < row; i++) 
    { 
        for (j = 0; j < col; j++) 
        { 
            if (i > j) 
            { 
                cout << "0" << " "; 
            } 
            else
            cout << matrix[i][j] << " "; 
        } 
        cout << endl; 
    } 
} 

// Driver Code 
int main() 
{ 
    int matrix[3][3] = {{1, 2, 3},  
                        {4, 5, 6},  
                        {7, 8, 9}}; 
    int row = 3, col = 3; 

    cout << "Lower triangular matrix: \n"; 
    lower(matrix, row, col); 

    cout << "Upper triangular matrix: \n"; 
    upper(matrix, row, col); 

    return 0; 
} 

```

## Java

```java

// Java program to print Lower  
// triangular and Upper triangular 
// matrix of an array 
class GFG 
{ 
    // method to form lower  
    // triangular matrix 
    static void lower(int matrix[][],  
                      int row, int col) 
    { 
        int i, j; 
        for (i = 0; i < row; i++) 
        { 
            for (j = 0; j < col; j++) 
            { 
                if (i < j) 
                { 
                    System.out.print("0" + " "); 
                } 
                else
                System.out.print(matrix[i][j] + " "); 
            } 
            System.out.println(); 
        } 
    } 

    // Method to form upper 
    // triangular matrix 
    static void upper(int matrix[][],  
                      int row, int col) 
    { 
        int i, j; 
        for (i = 0; i < row; i++) 
        { 
            for (j = 0; j < col; j++) 
            { 
                if (i > j) 
                { 
                    System.out.print("0" + " "); 
                } 
                else
                System.out.print(matrix[i][j] + " "); 
            } 
            System.out.println(); 
        } 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 
        int matrix[][] = {{1, 2, 3},  
                          {4, 5, 6},  
                          {7, 8, 9}}; 
        int row = 3, col = 3; 

        System.out.println("Lower triangular matrix: "); 
        lower(matrix, row, col); 

        System.out.println("Upper triangular matrix: "); 
        upper(matrix, row, col); 
    } 
} 

```

## Python3

```py

# Python3 program to print Lower  
# triangular and Upper triangular 
# matrix of an array 

# Function to form lower triangular  
# matrix 
def lower(matrix, row, col): 

    for i in range(0, row): 

        for j in range(0, col): 

            if (i < j): 

                print("0", end = " "); 

            else: 
                print(matrix[i][j],  
                       end = " " ); 

        print(" "); 

# Function to form upper triangular marix 
def upper(matrix, row, col): 

    for i in range(0, row): 

        for j in range(0, col): 

            if (i > j): 
                print("0", end = " "); 

            else: 
                print(matrix[i][j],  
                       end = " " ); 

        print(" "); 

# Driver Code 
matrix = [[1, 2, 3],  
          [4, 5, 6],  
          [7, 8, 9]]; 
row = 3; 
col = 3; 

print("Lower triangular matrix: "); 
lower(matrix, row, col); 

print("Upper triangular matrix: "); 
upper(matrix, row, col); 

# This code is contributed by 
# Shivi_Aggarwal  

```

## C# 

```cs

// C# program to print   
// Lower triangular and 
// Upper triangular 
// matrix of an array 
using System; 

class GFG 
{ 
    // method to form lower  
    // triangular matrix 
    static void lower(int [,]matrix,  
                      int row, int col) 
    { 
        int i, j; 
        for (i = 0; i < row; i++) 
        { 
            for (j = 0; j < col; j++) 
            { 
                if (i < j) 
                { 
                    Console.Write("0" + " "); 
                } 
                else
                Console.Write(matrix[i, j] + " "); 
            } 
            Console.WriteLine(); 
        } 
    } 

    // Method to form upper 
    // triangular matrix 
    static void upper(int [,]matrix,  
                      int row, int col) 
    { 
        int i, j; 
        for (i = 0; i < row; i++) 
        { 
            for (j = 0; j < col; j++) 
            { 
                if (i > j) 
                { 
                    Console.Write("0" + " "); 
                } 
                else
                Console.Write(matrix[i, j] + " "); 
            } 
        Console.WriteLine(); 
        } 
    } 

    // Driver Code 
    static public void Main () 
    { 
        int [,]matrix = {{1, 2, 3},  
                        {4, 5, 6},  
                        {7, 8, 9}}; 
        int row = 3, col = 3; 

        Console.WriteLine("Lower triangular matrix: "); 
        lower(matrix, row, col); 

        Console.WriteLine("Upper triangular matrix: "); 
        upper(matrix, row, col); 
    } 
} 

// This code is contributed by ajit  

```

## PHP

```php

<?php 
// PHP program to print Lower  
// triangular and Upper triangular 
// matrix of an array 

// Function to form  
// lower triangular matrix 
function lower($matrix, $row, $col) 
{ 
    $i; $j; 
    for ($i = 0; $i < $row; $i++) 
    { 
        for ($j = 0; $j < $col; $j++) 
        { 
            if ($i < $j) 
            { 
                echo "0" , " "; 
            } 
            else
            echo $matrix[$i][$j] , " "; 
        } 
        echo "\n"; 
    } 
} 

// Function to form 
// upper triangular marix 
function upper($matrix, $row, $col) 
{ 
    $i; $j; 

    for ($i = 0; $i < $row; $i++) 
    { 
        for ($j = 0; $j < $col; $j++) 
        { 
            if ($i > $j) 
            { 
                echo "0" , " "; 
            } 
            else
            echo $matrix[$i][$j] ," "; 
        } 
    echo "\n"; 
    } 
} 

// Driver Code 
$matrix = array (array (1, 2, 3), 
                  array (4, 5, 6), 
                 array (7, 8, 9)); 
$row = 3; $col = 3; 

echo "Lower triangular matrix: \n"; 
lower($matrix, $row, $col); 

echo "Upper triangular matrix: \n"; 
upper($matrix, $row, $col); 

// This code is contributed by jit_t 
?> 

```

**输出**：

```
Lower triangular matrix: 
1 0 0 
4 5 0 
7 8 9 
Upper triangular matrix: 
1 2 3 
0 5 6 
0 0 9 

```

