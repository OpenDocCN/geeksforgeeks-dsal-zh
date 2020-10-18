# 以反向螺旋形式打印给定的矩阵

> 原文： [https://www.geeksforgeeks.org/print-given-matrix-reverse-spiral-form/](https://www.geeksforgeeks.org/print-given-matrix-reverse-spiral-form/)

给定 2D 数组，以反向螺旋形式打印。 我们已经讨论过[以螺旋形式打印给定矩阵](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/)。 本文讨论了如何进行反向打印。 请参阅以下示例。

```
Input:
        1    2   3   4
        5    6   7   8
        9   10  11  12
        13  14  15  16
Output: 
10 11 7 6 5 9 13 14 15 16 12 8 4 3 2 1
Input:
        1   2   3   4  5   6
        7   8   9  10  11  12
        13  14  15 16  17  18
Output: 
11 10 9 8 7 13 14 15 16 17 18 12 6 5 4 3 2 1

```



## C++ 

```cpp

// This is a modified code of 
// https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/ 
#include <iostream> 
#define R 3 
#define C 6 
using namespace std; 

// Function that print matrix in reverse spiral form. 
void ReversespiralPrint(int m, int n, int a[R][C]) 
{ 
    // Large array to initialize it 
    // with elements of matrix 
    long int b[100]; 

    /* k - starting row index 
    l - starting column index*/
    int i, k = 0, l = 0; 

    // Counter for single dimension array 
    //in which elements will be stored 
    int z = 0; 

    // Total elements in matrix 
    int size = m*n; 

    while (k < m && l < n) 
    { 
        // Variable to store value of matrix. 
        int val; 

        /* Print the first row from the remaining rows */
        for (i = l; i < n; ++i) 
        { 
            // printf("%d ", a[k][i]); 
            val = a[k][i]; 
            b[z] = val; 
            ++z; 
        } 
        k++; 

        /* Print the last column from the remaining columns */
        for (i = k; i < m; ++i) 
        { 
            // printf("%d ", a[i][n-1]); 
            val = a[i][n-1]; 
            b[z] = val; 
            ++z; 
        } 
        n--; 

        /* Print the last row from the remaining rows */
        if ( k < m) 
        { 
            for (i = n-1; i >= l; --i) 
            { 
                // printf("%d ", a[m-1][i]); 
                val = a[m-1][i]; 
                b[z] = val; 
                ++z; 
            } 
            m--; 
        } 

        /* Print the first column from the remaining columns */
        if (l < n) 
        { 
            for (i = m-1; i >= k; --i) 
            { 
                // printf("%d ", a[i][l]); 
                val = a[i][l]; 
                b[z] = val; 
                ++z; 
            } 
            l++; 
        } 
    } 
    for (int i=size-1 ; i>=0 ; --i) 
    { 
        cout<<b[i]<<" "; 
    } 
} 

/* Driver program to test above functions */
int main() 
{ 
    int a[R][C] = { {1, 2, 3, 4, 5, 6}, 
                    {7, 8, 9, 10, 11, 12}, 
                    {13, 14, 15, 16, 17, 18}}; 
    ReversespiralPrint(R, C, a); 
    return 0; 
} 

```

## Java

```java

// JAVA Code for Print a given matrix in  
// reverse spiral form 
class GFG { 

    public static int R = 3, C = 6; 

    // Function that print matrix in reverse spiral form. 
    public static void ReversespiralPrint(int m, int n, 
                                             int a[][]) 
    { 
        // Large array to initialize it 
        // with elements of matrix 
        long b[] = new long[100]; 

        /* k - starting row index 
        l - starting column index*/
        int i, k = 0, l = 0; 

        // Counter for single dimension array 
        //in which elements will be stored 
        int z = 0; 

        // Total elements in matrix 
        int size = m * n; 

        while (k < m && l < n) 
        { 
            // Variable to store value of matrix. 
            int val; 

            /* Print the first row from the remaining  
            rows */
            for (i = l; i < n; ++i) 
            { 

                val = a[k][i]; 
                b[z] = val; 
                ++z; 
            } 
            k++; 

            /* Print the last column from the remaining 
            columns */
            for (i = k; i < m; ++i) 
            { 

                val = a[i][n-1]; 
                b[z] = val; 
                ++z; 
            } 
            n--; 

            /* Print the last row from the remaining  
            rows */
            if ( k < m) 
            { 
                for (i = n-1; i >= l; --i) 
                { 

                    val = a[m-1][i]; 
                    b[z] = val; 
                    ++z; 
                } 
                m--; 
            } 

            /* Print the first column from the remaining  
            columns */
            if (l < n) 
            { 
                for (i = m-1; i >= k; --i) 
                { 

                    val = a[i][l]; 
                    b[z] = val; 
                    ++z; 
                } 
                l++; 
            } 
        } 

        for (int x = size-1 ; x>=0 ; --x) 
        { 
            System.out.print(b[x]+" "); 
        } 
    }     

    /* Driver program to test above function */
    public static void main(String[] args)  
    { 
        int a[][] = { {1, 2, 3, 4, 5, 6}, 
                    {7, 8, 9, 10, 11, 12}, 
                    {13, 14, 15, 16, 17, 18}}; 

        ReversespiralPrint(R, C, a); 

    } 
  } 
// This code is contributed by Arnav Kr. Mandal. 

```

## Python3

```py

# Python3 Code to Print a given   
# matrix in reverse spiral form 

# This is a modified code of 
# https:#www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/ 
R, C = 3, 6

def ReversespiralPrint(m, n, a): 

    # Large array to initialize it 
    # with elements of matrix 
    b = [0 for i in range(100)] 

    #/* k - starting row index 
    #l - starting column index*/ 
    i, k, l = 0, 0, 0

    # Counter for single dimension array 
    # in which elements will be stored 
    z = 0

    # Total elements in matrix 
    size = m * n 

    while (k < m and l < n): 

        # Variable to store value of matrix. 
        val = 0

        # Print the first row  
        # from the remaining rows  
        for i in range(l, n): 

            # printf("%d ", a[k][i]) 
            val = a[k][i] 
            b[z] = val 
            z += 1
        k += 1

        # Print the last column 
        # from the remaining columns 
        for i in range(k, m): 

            # printf("%d ", a[i][n-1]) 
            val = a[i][n - 1] 
            b[z] = val 
            z += 1

        n -= 1

        # Print the last row  
        # from the remaining rows 
        if (k < m): 
            for i in range(n - 1, l - 1, -1): 

                # printf("%d ", a[m-1][i]) 
                val = a[m - 1][i] 
                b[z] = val 
                z += 1

        m -= 1

        # Print the first column  
        # from the remaining columns  
        if (l < n): 
            for i in range(m - 1, k - 1, -1): 

                # printf("%d ", a[i][l]) 
                val = a[i][l] 
                b[z] = val 
                z += 1
            l += 1

    for i in range(size - 1, -1, -1): 
        print(b[i], end = " ") 

# Driver Code 
a = [[1, 2, 3, 4, 5, 6], 
     [7, 8, 9, 10, 11, 12], 
     [13, 14, 15, 16, 17, 18]] 

ReversespiralPrint(R, C, a) 

# This code is contributed by mohit kumar 

```

## C# 

```cs

// C# Code for Print a given matrix in  
// reverse spiral form 
using System; 
class GFG { 

    public static int R = 3, C = 6; 

    // Function that print matrix in reverse spiral form. 
    public static void ReversespiralPrint(int m, int n, 
                                            int [,]a) 
    { 
        // Large array to initialize it 
        // with elements of matrix 
        long []b = new long[100]; 

        /* k - starting row index 
        l - starting column index*/
        int i, k = 0, l = 0; 

        // Counter for single dimension array 
        //in which elements will be stored 
        int z = 0; 

        // Total elements in matrix 
        int size = m * n; 

        while (k < m && l < n) 
        { 
            // Variable to store value of matrix. 
            int val; 

            /* Print the first row from the remaining  
            rows */
            for (i = l; i < n; ++i) 
            { 

                val = a[k,i]; 
                b[z] = val; 
                ++z; 
            } 
            k++; 

            /* Print the last column from the remaining 
            columns */
            for (i = k; i < m; ++i) 
            { 

                val = a[i,n-1]; 
                b[z] = val; 
                ++z; 
            } 
            n--; 

            /* Print the last row from the remaining  
            rows */
            if ( k < m) 
            { 
                for (i = n-1; i >= l; --i) 
                { 

                    val = a[m-1,i]; 
                    b[z] = val; 
                    ++z; 
                } 
                m--; 
            } 

            /* Print the first column from the remaining  
            columns */
            if (l < n) 
            { 
                for (i = m-1; i >= k; --i) 
                { 

                    val = a[i,l]; 
                    b[z] = val; 
                    ++z; 
                } 
                l++; 
            } 
        } 

        for (int x = size-1 ; x>=0 ; --x) 
        { 
        Console.Write(b[x]+" "); 
        } 
    }  

    /* Driver program to test above function */
    public static void Main()  
    { 
        int [ ,]a = { {1, 2, 3, 4, 5, 6}, 
                    {7, 8, 9, 10, 11, 12}, 
                    {13, 14, 15, 16, 17, 18}}; 

        ReversespiralPrint(R, C, a); 

    } 
} 
// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP Code for Print a given   
// matrix in reverse spiral form 
$R=3; 
$C=6; 

// Function that print matrix  
// in reverse spiral form. 
function ReversespiralPrint($m, $n, array $a) 
{ 

    // Large array to initialize it 
    // with elements of matrix 
    $b; 

    // k - starting row index 
    // l - starting column index 
    $k = 0; 
    $l = 0; 

    // Counter for single dimension array 
    // in which elements will be stored 
    $z = 0; 

    // Total elements in matrix 
    $size = $m*$n; 

    while ($k < $m && $l < $n) 
    { 

        // Variable to store 
        // value of matrix. 
        $val; 

        // Print the first row from  
        // the remaining rows 
        for ($i = $l; $i < $n; ++$i) 
        { 
            $val = $a[$k][$i]; 
            $b[$z] = $val; 
            ++$z; 
        } 
        $k++; 

        // Print the last column from 
        // the remaining columns  
        for ($i = $k; $i < $m; ++$i) 
        { 

            // printf("%d ", a[i][n-1]); 
            $val = $a[$i][$n-1]; 
            $b[$z] = $val; 
            ++$z; 
        } 
        $n--; 

        // Print the last row from  
        // the remaining rows 
        if ( $k < $m) 
        { 
            for ($i = $n-1; $i >= $l; --$i) 
            { 

                // printf("%d ", a[m-1][i]); 
                $val = $a[$m-1][$i]; 
                $b[$z] = $val; 
                ++$z; 
            } 
            $m--; 
        } 

        // Print the first column  
        // from the remaining columns  
        if ($l < $n) 
        { 
            for ($i = $m - 1; $i >= $k; --$i) 
            { 
                $val = $a[$i][$l]; 
                $b[$z] = $val; 
                ++$z; 
            } 
            $l++; 
        } 
    } 
    for ($i = $size - 1; $i >= 0; --$i) 
    { 
        echo $b[$i]." "; 
    } 
} 

    // Driver Code 
    $a= array(array(1, 2, 3, 4, 5, 6), 
              array(7, 8, 9, 10, 11, 12), 
              array(13, 14, 15, 16, 17, 18)); 
    ReversespiralPrint($R, $C, $a); 

// This Code is contributed by mits  
?> 

```

**输出**：

```
11 10 9 8 7 13 14 15 16 17 18 12 6 5 4 3 2 1

```

