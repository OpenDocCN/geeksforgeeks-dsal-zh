# 程序检查矩阵是否为上三角

> 原文： [https://www.geeksforgeeks.org/program-check-matrix-upper-triangular/](https://www.geeksforgeeks.org/program-check-matrix-upper-triangular/)

给定一个正方形矩阵，任务是检查矩阵是否为上三角形式。 如果主对角线以下的所有条目均为零，则方阵称为上三角。

![](img/aec884395a5633faf9dd50e65feda1dc.png)

例子：

```
Input : mat[4][4] = {{1, 3, 5, 3},
                     {0, 4, 6, 2},
                     {0, 0, 2, 5},
                     {0, 0, 0, 6}};
Output : Matrix is in Upper Triangular form.

Input : mat[4][4] = {{5, 6, 3, 6},
                     {0, 4, 6, 6},
                     {1, 0, 8, 5},
                     {0, 1, 0, 6}};
Output : Matrix is not in Upper Triangular form.

```



## C++ 

```cpp

// Program to check upper triangular matrix. 
#include <bits/stdc++.h> 
#define N 4 
using namespace std; 

// Function to check matrix is in upper triangular 
// form or not. 
bool isUpperTriangularMatrix(int mat[N][N]) 
{ 
    for (int i = 1; i < N; i++) 
        for (int j = 0; j < i; j++) 
            if (mat[i][j] != 0) 
                return false; 
    return true; 
} 

// Driver function. 
int main() 
{ 
    int mat[N][N] = { { 1, 3, 5, 3 }, 
                      { 0, 4, 6, 2 }, 
                      { 0, 0, 2, 5 }, 
                      { 0, 0, 0, 6 } }; 
    if (isUpperTriangularMatrix(mat)) 
        cout << "Yes"; 
    else
        cout << "No"; 
    return 0; 
} 

```

## Java

```java

// Java Program to check upper  
// triangular matrix. 
import java.util.*; 
import java.lang.*; 

public class GfG 
{ 
    private static final int N = 4; 

    // Function to check matrix is in 
    // upper triangular form or not. 
    public static Boolean isUpperTriangularMatrix(int mat[][]) 
    { 
        for (int i = 1; i < N ; i++) 
            for (int j = 0; j < i; j++) 
                if (mat[i][j] != 0) 
                    return false; 
        return true; 
    }  

    // driver function 
    public static void main(String argc[]){ 
        int[][] mat= { { 1, 3, 5, 3 }, 
                       { 0, 4, 6, 2 }, 
                       { 0, 0, 2, 5 }, 
                       { 0, 0, 0, 6 } }; 

        if (isUpperTriangularMatrix(mat)) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 
    } 
} 

/* This code is contributed by Sagar Shukla */

```

## Python3

```py

# Python3 Program to check upper  
# triangular matrix. 

# Function to check matrix  
# is in upper triangular 
def isuppertriangular(M): 
    for i in range(1, len(M)): 
        for j in range(0, i): 
            if(M[i][j] != 0):  
                    return False
    return True

# Driver function. 
M = [[1,3,5,3], 
    [0,4,6,2], 
    [0,0,2,5], 
    [0,0,0,6]] 

if isuppertriangular(M): 
    print ("Yes") 
else: 
    print ("No") 

# This code is contributed by Anurag Rawat 

```

## C# 

```cs

// C# Program to check upper  
// triangular matrix. 
using System; 

public class GfG 
{ 
    private static int N = 4; 

    // Function to check matrix is in 
    // upper triangular form or not. 
    public static bool isUpperTriangularMatrix(int [,]mat) 
    { 
        for (int i = 1; i < N ; i++) 
            for (int j = 0; j < i; j++) 
                if (mat[i, j] != 0) 
                    return false; 
        return true; 
    }  

    // Driver function 
    public static void Main(){ 
        int [,]mat= { { 1, 3, 5, 3 }, 
                    { 0, 4, 6, 2 }, 
                    { 0, 0, 2, 5 }, 
                    { 0, 0, 0, 6 } }; 

        if (isUpperTriangularMatrix(mat)) 
            Console.WriteLine("Yes"); 
        else
            Console.WriteLine("No"); 
    } 
} 

/* This code is contributed by vt_m */

```

## PHP

```php

<?php 
// PHP Program to check upper  
// triangular matrix. 
$N = 4; 

// Function to check matrix is  
// in upper triangular form or 
// not. 
function isUpperTriangularMatrix($mat) 
{ 
    global $N; 
    for ($i = 1; $i < $N; $i++) 
        for ($j = 0; $j < $i; $j++) 
            if ($mat[$i][$j] != 0) 
                return false; 
    return true; 
} 

    // Driver Code 
    $mat = array(array(1, 3, 5, 3), 
                 array(0, 4, 6, 2) , 
                 array(0, 0, 2, 5), 
                 array(0, 0, 0, 6)); 

    if (isUpperTriangularMatrix($mat)) 
        echo "Yes"; 
    else
        echo"No"; 

// This code is contributed by anuj_67\. 
?> 

```

Output:

```
Yes
```



* * *

* * *



