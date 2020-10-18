# 在按行和按列排序的矩阵中计数零

> 原文： [https://www.geeksforgeeks.org/count-zeros-in-a-row-wise-and-column-wise-sorted-matrix/](https://www.geeksforgeeks.org/count-zeros-in-a-row-wise-and-column-wise-sorted-matrix/)

给定一个`N x N`的二进制矩阵（矩阵中的元素可以为 1 或 0），其中矩阵的每一行和每一列都按升序排序，其中计数为 0。

预期时间复杂度为`O(n)`。

**示例**：

```
Input: 
[0, 0, 0, 0, 1]
[0, 0, 0, 1, 1]
[0, 1, 1, 1, 1]
[1, 1, 1, 1, 1]
[1, 1, 1, 1, 1]

Output: 8

Input: 
[0, 0]
[0, 0]

Output: 4

Input: 
[1, 1, 1, 1]
[1, 1, 1, 1]
[1, 1, 1, 1]
[1, 1, 1, 1]

Output: 0

```



这个想法很简单。 我们从矩阵的左下角开始，然后重复以下步骤，直到找到矩阵的顶部或右侧。

1.  递减行索引，直到找到 0。

2.  在当前列中添加 0 数，即当前行索引加 1，然后向右移至下一列（将列索引递增 1）。

由于矩阵是按行和按列排序的，因此上述逻辑将起作用。 该逻辑也适用于任何包含非负整数的矩阵。

下面是上述想法的实现：

## C++ 

```cpp

// C++ program to count number of 0s in the given 
// row-wise and column-wise sorted binary matrix. 
#include <iostream> 
using namespace std; 
// define size of square matrix 
#define N 5 

// Function to count number of 0s in the given 
// row-wise and column-wise sorted binary matrix. 
int countZeroes(int mat[N][N]) 
{ 
    // start from bottom-left corner of the matrix 
    int row = N - 1, col = 0; 

    // stores number of zeroes in the matrix 
    int count = 0; 

    while (col < N) 
    { 
        // move up until you find a 0 
        while (mat[row][col]) 

            // if zero is not found in current column, 
            // we are done 
            if (--row < 0) 
                return count; 

        // add 0s present in current column to result 
        count += (row + 1); 

        // move right to next column 
        col++; 
    } 

    return count; 
} 

// Driver Program to test above functions 
int main() 
{ 
    int mat[N][N] = 
    { 
        { 0, 0, 0, 0, 1 }, 
        { 0, 0, 0, 1, 1 }, 
        { 0, 1, 1, 1, 1 }, 
        { 1, 1, 1, 1, 1 }, 
        { 1, 1, 1, 1, 1 } 
    }; 

    cout << countZeroes(mat); 

    return 0; 
} 

```

## Java

```java

// Java program to count number of 0s in the given 
// row-wise and column-wise sorted binary matrix 
import java.io.*; 

class GFG  
{ 
    public static int N = 5; 

    // Function to count number of 0s in the given 
    // row-wise and column-wise sorted binary matrix. 
    static int countZeroes(int mat[][]) 
    { 
        // start from bottom-left corner of the matrix 
        int row = N - 1, col = 0; 

        // stores number of zeroes in the matrix 
        int count = 0; 

        while (col < N) 
        { 
            // move up until you find a 0 
            while (mat[row][col] > 0) 

                // if zero is not found in current column, 
                // we are done 
                if (--row < 0) 
                    return count; 

            // add 0s present in current column to result 
            count += (row + 1); 

            // move right to next column 
            col++; 
        } 

        return count; 
    } 

    // Driver program 
    public static void main (String[] args)  
    { 
        int mat[][] = { { 0, 0, 0, 0, 1 }, 
                        { 0, 0, 0, 1, 1 }, 
                        { 0, 1, 1, 1, 1 }, 
                        { 1, 1, 1, 1, 1 }, 
                        { 1, 1, 1, 1, 1 } }; 
        System.out.println(countZeroes(mat)); 
    } 
} 

// This code is contributed by Pramod Kumar 

```

## Python

```

# Python program to count number  
# of 0s in the given row-wise 
# and column-wise sorted  
# binary matrix. 

# Function to count number  
# of 0s in the given 
# row-wise and column-wise 
# sorted binary matrix. 
def countZeroes(mat): 

    # start from bottom-left 
    # corner of the matrix 
    N = 5; 
    row = N - 1; 
    col = 0; 

    # stores number of  
    # zeroes in the matrix 
    count = 0; 

    while (col < N): 

        # move up until 
        # you find a 0 
        while (mat[row][col]): 

            # if zero is not found  
            # in current column, we  
            # are done 
            if (row < 0): 
                return count; 
            row = row - 1; 

        # add 0s present in 
        # current column to result 
        count = count + (row + 1); 

        # move right to 
        # next column 
        col = col + 1; 

    return count; 

# Driver Code 
mat = [[0, 0, 0, 0, 1], 
       [0, 0, 0, 1, 1], 
       [0, 1, 1, 1, 1], 
       [1, 1, 1, 1, 1], 
       [1, 1, 1, 1, 1]]; 

print( countZeroes(mat)); 

# This code is contributed 
# by chandan_jnu  

```

## C# 

```cs

// C# program to count number of 
// 0s in the given row-wise and 
// column-wise sorted binary matrix 
using System; 

class GFG  
{ 
    public static int N = 5; 

    // Function to count number of  
    // 0s in the given row-wise and 
    // column-wise sorted binary matrix. 
    static int countZeroes(int [,] mat) 
    { 
        // start from bottom-left 
        // corner of the matrix 
        int row = N - 1, col = 0; 

        // stores number of zeroes  
        // in the matrix 
        int count = 0; 

        while (col < N) 
        { 
            // move up until you find a 0 
            while (mat[row,col] > 0) 

                // if zero is not found in  
                // current column, 
                // we are done 
                if (--row < 0) 
                    return count; 

            // add 0s present in current  
            // column to result 
            count += (row + 1); 

            // move right to next column 
            col++; 
        } 

        return count; 
    } 

    // Driver Code 
    public static void Main ()  
    { 
        int [,] mat = { { 0, 0, 0, 0, 1 }, 
                        { 0, 0, 0, 1, 1 }, 
                        { 0, 1, 1, 1, 1 }, 
                        { 1, 1, 1, 1, 1 }, 
                        { 1, 1, 1, 1, 1 } }; 
        Console.WriteLine(countZeroes(mat)); 
    } 
} 

// This code is contributed by KRV. 

```

## PHP

```php

<?php 
// PHP program to count number  
// of 0s in the given row-wise 
// and column-wise sorted  
// binary matrix. 

// Function to count number  
// of 0s in the given 
// row-wise and column-wise 
// sorted binary matrix. 
function countZeroes($mat) 
{ 
    // start from bottom-left 
    // corner of the matrix 
    $N = 5; 
    $row = $N - 1; 
    $col = 0; 

    // stores number of  
    // zeroes in the matrix 
    $count = 0; 

    while ($col < $N) 
    { 
        // move up until 
        // you find a 0 
        while ($mat[$row][$col]) 

            // if zero is not found  
            // in current column, we  
            // are done 
            if (--$row < 0) 
                return $count; 

        // add 0s present in 
        // current column to result 
        $count += ($row + 1); 

        // move right to 
        // next column 
        $col++; 
    } 

    return $count; 
} 

// Driver Code 
$mat = array(array(0, 0, 0, 0, 1), 
             array(0, 0, 0, 1, 1), 
             array(0, 1, 1, 1, 1), 
             array(1, 1, 1, 1, 1), 
             array(1, 1, 1, 1, 1)); 

echo countZeroes($mat); 

// This code is contributed by Sam007 
?> 

```

**输出**：

```
8

```

**上述解决方案的时间复杂度**为`O(n)`，因为解决方案遵循从矩阵的左下角到顶部或右侧的单个路径。

**程序使用的辅助空间**为`O(1)`。

如果您发现解决此问题的更多有趣方法，请与我们分享。

