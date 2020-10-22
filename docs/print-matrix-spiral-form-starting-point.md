# 从起始点以螺旋形式打印矩阵

> 原文： [https://www.geeksforgeeks.org/print-matrix-spiral-form-starting-point/](https://www.geeksforgeeks.org/print-matrix-spiral-form-starting-point/)

给定大小为`n * m`的矩阵和点`P(c, r)`。 从点`P`开始以螺旋形式（顺时针）打印矩阵。

**示例**：

```
Input : mat[][] = {{1 2 3},
                   {4 5 6},
                   {7 8 9}}
        Point P = (0, 2)
Output : 3 6 5 2 9 8 7 4 1
The starting point is top left which
is 3.

```



这个问题主要是[以螺旋形式](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/)打印矩阵的扩展。

## C++ 

```cpp

// C++ program to print a matrix in spiral 
// form. 
#include <iostream> 
using namespace std; 

const int MAX = 100; 

void printSpiral(int mat[][MAX], int r, int c) 
{ 

    int i, a = 0, b = 2; 

    int low_row = (0 > a) ? 0 : a; 
    int low_column = (0 > b) ? 0 : b - 1; 
    int high_row = ((a + 1) >= r) ? r - 1 : a + 1; 
    int high_column = ((b + 1) >= c) ? c - 1 : b + 1; 

    while ((low_row > 0 - r && low_column > 0 - c)) { 

        for (i = low_column + 1; i <= high_column &&  
                         i < c && low_row >= 0; ++i) 
            cout << mat[low_row][i] << " "; 
        low_row -= 1; 

        for (i = low_row + 2; i <= high_row && i < r &&  
                                   high_column < c; ++i) 
            cout << mat[i][high_column] << " "; 
        high_column += 1; 

        for (i = high_column - 2; i >= low_column && 
                               i >= 0 && high_row < r; --i) 
            cout << mat[high_row][i] << " "; 
        high_row += 1; 

        for (i = high_row - 2; i > low_row && i >= 0  
                                   && low_column >= 0; --i) 
            cout << mat[i][low_column] << " "; 
        low_column -= 1; 
    } 
    cout << endl; 
} 

// Driver code 
int main() 
{ 
    int mat[][MAX] = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } }; 
    int r = 3, c = 3; 

    printSpiral(mat, r, c); 
} 

```

## Java

```java

// Java program to print a 
// matrix in spiral form 
import java.io.*; 

class GFG { 

static void printSpiral(int [][]mat, int r, int c) 
{ 
    int i, a = 0, b = 2; 

    int low_row = (0 > a) ? 0 : a; 
    int low_column = (0 > b) ? 0 : b - 1; 
    int high_row = ((a + 1) >= r) ? r - 1 : a + 1; 
    int high_column = ((b + 1) >= c) ? c - 1 : b + 1; 

    while ((low_row > 0 - r && low_column > 0 - c))  
    { 
        for (i = low_column + 1; i <= high_column &&  
                         i < c && low_row >= 0; ++i) 
            System.out.print (mat[low_row][i] + " "); 
        low_row -= 1; 

        for (i = low_row + 2; i <= high_row && i < r &&  
                                  high_column < c; ++i) 
            System.out.print(mat[i][high_column] + " "); 
        high_column += 1; 

        for (i = high_column - 2; i >= low_column && 
                        i >= 0 && high_row < r; --i) 
            System.out.print(mat[high_row][i] + " "); 
        high_row += 1; 

        for (i = high_row - 2; i > low_row && i >= 0
                            && low_column >= 0; --i) 
            System.out.print(mat[i][low_column] +" "); 
        low_column -= 1; 
    } 
    System.out.println(); 
} 

// Driver code 
    static public void main (String[] args) 
    { 
        int [][]mat = {{1, 2, 3}, 
                       {4, 5, 6},  
                       {7, 8, 9}}; 
        int r = 3, c = 3; 

        // Function calling 
        printSpiral(mat, r, c); 
    } 
} 

// This code is contributed by vt_m. 

```

## Python 3

```py

# Python3 program to print a matrix  
# in spiral form. 
MAX = 100

def printSpiral(mat, r, c): 

    a = 0
    b = 2

    low_row = 0 if (0 > a) else a 
    low_column = 0 if (0 > b) else b - 1
    high_row = r-1 if ((a + 1) >= r) else a + 1
    high_column = c-1 if ((b + 1) >= c) else b + 1

    while ((low_row > 0 - r and low_column > 0 - c)): 

        i = low_column + 1
        while (i <= high_column and 
               i < c and low_row >= 0): 
            print( mat[low_row][i], end = " ") 
            i += 1
        low_row -= 1

        i = low_row + 2
        while (i <= high_row and
               i < r and high_column < c): 
            print(mat[i][high_column], end = " ") 
            i += 1
        high_column += 1

        i = high_column - 2
        while (i >= low_column and 
               i >= 0 and high_row < r): 
            print(mat[high_row][i], end = " ") 
            i -= 1
        high_row += 1

        i = high_row - 2
        while (i > low_row and 
               i >= 0 and low_column >= 0): 
            print(mat[i][low_column], end = " ") 
            i -= 1
        low_column -= 1

    print() 

# Driver code 
if __name__ == "__main__": 

    mat = [[ 1, 2, 3 ],  
           [ 4, 5, 6 ],  
           [ 7, 8, 9 ]] 
    r = 3
    c = 3
    printSpiral(mat, r, c) 

# This code is contributed by ita_c 

```

## C# 

```cs

// C# program to print a  
// matrix in spiral form 
using System; 

class GFG { 

static void printSpiral(int [,]mat, int r, int c) 
{ 
    int i, a = 0, b = 2; 

    int low_row = (0 > a) ? 0 : a; 
    int low_column = (0 > b) ? 0 : b - 1; 
    int high_row = ((a + 1) >= r) ? r - 1 : a + 1; 
    int high_column = ((b + 1) >= c) ? c - 1 : b + 1; 

    while ((low_row > 0 - r && low_column > 0 - c)) 
    { 
        for (i = low_column + 1; i <= high_column &&  
                         i < c && low_row >= 0; ++i) 
            Console.Write (mat[low_row,i] + " "); 
        low_row -= 1; 

        for (i = low_row + 2; i <= high_row && i < r &&  
                                  high_column < c; ++i) 
            Console.Write(mat[i,high_column] + " "); 
        high_column += 1; 

        for (i = high_column - 2; i >= low_column && 
                        i >= 0 && high_row < r; --i) 
            Console.Write(mat[high_row,i] + " "); 
        high_row += 1; 

        for (i = high_row - 2; i > low_row && i >= 0  
                            && low_column >= 0; --i) 
            Console.Write(mat[i,low_column] +" "); 
        low_column -= 1; 
    } 
    Console.WriteLine(); 
} 

    // Driver code 
    static public void Main () 
    { 
        int [,]mat = {{1, 2, 3}, 
                      {4, 5, 6},  
                      {7, 8, 9}}; 
        int r = 3, c = 3; 

        // Function calling 
        printSpiral(mat, r, c); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP program to print a  
// matrix in spiral form. 
$MAX = 100; 

function printSpiral($mat,  
                     $r, $c) 
{ 
    global $MAX; 
    $i; $a = 0; $b = 2; 

    $low_row = (0 > $a) ?  
                0 : $a; 
    $low_column = (0 > $b) ?  
                   0 : $b - 1; 
    $high_row = (($a + 1) >= $r) ?  
                  $r - 1 : $a + 1; 
    $high_column = (($b + 1) >= $c) ?  
                     $c - 1 : $b + 1; 

    while (($low_row > 0 - $r &&  
            $low_column > 0 - $c)) 
    { 

        for ($i = $low_column + 1;  
             $i <= $high_column &&  
             $i < $c && $low_row >= 0; ++$i) 
            echo $mat[$low_row][$i], " "; 
        $low_row -= 1; 

        for ($i = $low_row + 2;  
             $i <= $high_row && $i < $r &&  
             $high_column < $c; ++$i) 
        echo $mat[$i][$high_column] , " "; 
        $high_column += 1; 

        for ($i = $high_column - 2;  
             $i >= $low_column && 
             $i >= 0 && $high_row < $r; --$i) 
            echo $mat[$high_row][$i] , " "; 
        $high_row += 1; 

        for ($i = $high_row - 2;  
             $i > $low_row && $i >= 0 &&  
             $low_column >= 0; --$i) 
            echo $mat[$i][$low_column] , " "; 
        $low_column -= 1; 
    } 
    echo "\n"; 
} 

// Driver code 
$mat = array(array(1, 2, 3), 
             array(4, 5, 6), 
             array(7, 8, 9)); 
$r = 3; $c = 3; 

printSpiral($mat, $r, $c); 

// This code is contributed by aj_36 
?> 

```

**输出**：

```
3 6 5 2 9 8 7 4 1

```

