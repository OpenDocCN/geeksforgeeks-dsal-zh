# 检查幂等矩阵的程序

> 原文： [https://www.geeksforgeeks.org/program-check-idempotent-matrix/](https://www.geeksforgeeks.org/program-check-idempotent-matrix/)

给定一个`N * N`矩阵，任务是检查矩阵是否为幂等矩阵。

[**幂等矩阵**](https://en.wikipedia.org/wiki/Idempotent_matrix)：如果矩阵与自身相乘返回相同的矩阵，则称该矩阵为幂等矩阵。 当且仅当`M * M = M`时，矩阵`M`才是幂等矩阵。 在幂等矩阵中，`M`是方阵。

![idempotent matrix](img/8f86cce9b07f210db176de40f0d9888b.png)

例子：

```
Input : mat[][] = {{3, -6},
                   {1, -2}};
Output : Idempotent Matrix

Input : mat[N][N] = {{2, -2, -4},
                     {-1, 3, 4},
                     {1, -2, -3}}
Output : Idempotent Matrix.

```



## C++ 

```cpp

// Program to check given matrix  
// is idempotent matrix or not. 
#include<bits/stdc++.h> 
#define N 3 
using namespace std; 

// Function for matrix multiplication. 
void multiply(int mat[][N], int res[][N]) 
{ 
    for (int i = 0; i < N; i++) 
    { 
        for (int j = 0; j < N; j++) 
        { 
            res[i][j] = 0; 
            for (int k = 0; k < N; k++) 
                res[i][j] += mat[i][k] * mat[k][j]; 
        } 
    } 
} 

// Function to check idempotent 
// property of matrix. 
bool checkIdempotent(int mat[][N]) 
{    
    // Calculate multiplication of matrix 
    // with itself and store it into res. 
    int res[N][N]; 
    multiply(mat, res); 

    for (int i = 0; i < N; i++)     
        for (int j = 0; j < N; j++)         
            if (mat[i][j] != res[i][j]) 
                return false; 
    return true; 
} 

// Driver function. 
int main() 
{ 
    int mat[N][N] = {{2, -2, -4}, 
                    {-1, 3, 4}, 
                    {1, -2, -3}}; 

    // checkIdempotent function call. 
    if (checkIdempotent(mat)) 
        cout << "Idempotent Matrix"; 
    else
        cout << "Not Idempotent Matrix."; 
    return 0; 
} 

```

## Java

```java

// Java program to check given matrix  
// is idempotent matrix or not. 
import java.io.*; 

class GFG  
{ 
    static int N = 3; 

    // Function for matrix multiplication. 
    static void multiply(int mat[][], int res[][]) 
    { 
        for (int i = 0; i < N; i++) 
        { 
            for (int j = 0; j < N; j++) 
            { 
                res[i][j] = 0; 
                for (int k = 0; k < N; k++) 
                    res[i][j] += mat[i][k] * mat[k][j]; 
            } 
        } 
    } 

    // Function to check idempotent 
    // property of matrix. 
    static boolean checkIdempotent(int mat[][]) 
    {  
        // Calculate multiplication of matrix 
        // with itself and store it into res. 
        int res[][] = new int[N][N]; 
        multiply(mat, res); 

        for (int i = 0; i < N; i++) 
        {  
            for (int j = 0; j < N; j++) 
            { 
                if (mat[i][j] != res[i][j]) 
                    return false; 
            } 
        } 
        return true; 
    } 

    // Driver code. 
    public static void main (String[] args)  
    { 
        int mat[][] = {{2, -2, -4}, 
                       {-1, 3, 4}, 
                       {1, -2, -3}}; 

        // checkIdempotent function call. 
        if (checkIdempotent(mat)) 
            System.out.println( "Idempotent Matrix"); 
        else
            System.out.println("Not Idempotent Matrix."); 

    } 
} 

// This code is contributed by vt_m. 

```

## Python 3

```py

# Python Program to check given matrix  
# is idempotent matrix or not. 
import math 

# Function for matrix multiplication. 
def multiply(mat, res): 

    N= len(mat) 
    for i in range(0,N): 

        for j in range(0,N): 

            res[i][j] = 0
            for k in range(0,N): 
                res[i][j] += mat[i][k] * mat[k][j] 

# Function to check idempotent 
# property of matrix. 
def checkIdempotent(mat): 

    N= len(mat) 
    # Calculate multiplication of matrix 
    # with itself and store it into res. 
    res =[[0]*N for i in range(0,N)] 
    multiply(mat, res) 

    for i in range(0,N): 
        for j in range(0,N):      
            if (mat[i][j] != res[i][j]): 
                return False
    return True

# driver Function 
mat = [ [2, -2, -4], 
        [-1, 3, 4], 
        [1, -2, -3] ] 

# checkIdempotent function call. 
if (checkIdempotent(mat)): 
    print("Idempotent Matrix") 
else: 
    print("Not Idempotent Matrix.") 

# This code is contributed by Gitanjali. 

```

## C# 

```cs

// C# program to check given matrix  
// is idempotent matrix or not. 
using System; 

class GFG  
{ 
    static int N = 3; 

    // Function for matrix multiplication. 
    static void multiply(int [,]mat, int [,]res) 
    { 
        for (int i = 0; i < N; i++) 
        { 
            for (int j = 0; j < N; j++) 
            { 
                res[i,j] = 0; 
                for (int k = 0; k < N; k++) 
                    res[i,j] += mat[i,k] * mat[k,j]; 
            } 
        } 
    } 

    // Function to check idempotent 
    // property of matrix. 
    static bool checkIdempotent(int [,]mat) 
    {  
        // Calculate multiplication of matrix 
        // with itself and store it into res. 
        int [,]res = new int[N,N]; 
        multiply(mat, res); 

        for (int i = 0; i < N; i++) 
        {  
            for (int j = 0; j < N; j++) 
            { 
                if (mat[i,j] != res[i,j]) 
                    return false; 
            } 
        } 
        return true; 
    } 

    // Driver code 
    public static void Main ()  
    { 
        int [,]mat = {{2, -2, 4}, 
                    {-1, 3, 4}, 
                    {1, -2, -3}}; 

        // checkIdempotent function call. 
        if (checkIdempotent(mat)) 
            Console.WriteLine( "Idempotent Matrix"); 
        else
            Console.WriteLine("Not Idempotent Matrix."); 

    } 
} 

// This code is contributed by vt_m. 

```

Output

```
Idempotent Matrix
```



* * *

* * *



