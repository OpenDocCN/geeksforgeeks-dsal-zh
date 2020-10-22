# 方阵中的最大值和最小值

> 原文： [https://www.geeksforgeeks.org/maximum-and-minimum-in-a-square-matrix/](https://www.geeksforgeeks.org/maximum-and-minimum-in-a-square-matrix/)

给定`n * n`阶方阵，从给定的矩阵中找到最大值和最小值。

**示例**：

```
Input : arr[][] = {5, 4, 9,
                   2, 0, 6,
                   3, 1, 8};
Output : Maximum = 9, Minimum = 0

Input : arr[][] = {-5, 3, 
                   2, 4};
Output : Maximum = 4, Minimum = -5

```



**朴素的方法**：

我们使用线性搜索分别找到矩阵的最大值和最小值。 所需的比较数是`n ^ 2`用于找到最小值，`n ^ 2`用于找到最大值元素。 总比较等于`2n ^ 2`。

**对比较（有效方法）**：

从矩阵中选择两个元素，一个从矩阵行的开头选择，另一个从矩阵同一行的结尾选择，比较它们，然后将它们的较小值与矩阵的最小值比较小，将它们的较大值与矩阵的最大值比较。 我们可以看到，对于两个元素，我们需要 3 比较，因此对于遍历整个矩阵，我们总共需要`3/2 n ^ 2`比较。

**注意**：这是[最大数组最小值的方法 3 的扩展形式](https://www.geeksforgeeks.org/maximum-and-minimum-in-an-array/)。

## C++ 

```cpp

// C++ program for finding maximum and minimum in 
// a matrix. 
#include<bits/stdc++.h> 
using namespace std; 

#define MAX 100 

// Finds maximum and minimum in arr[0..n-1][0..n-1] 
// using pair wise comparisons 
void maxMin(int arr[][MAX], int n) 
{ 
    int min = INT_MAX; 
    int max = INT_MIN; 

    // Traverses rows one by one 
    for (int i = 0; i < n; i++) 
    { 
        for (int j = 0; j <= n/2; j++) 
        { 
            // Compare elements from beginning 
            // and end of current row 
            if (arr[i][j] > arr[i][n-j-1]) 
            { 
                if (min > arr[i][n-j-1]) 
                    min = arr[i][n-j-1]; 
                if (max< arr[i][j]) 
                    max = arr[i][j]; 
            } 
            else
            { 
                if (min > arr[i][j]) 
                    min = arr[i][j]; 
                if (max< arr[i][n-j-1]) 
                    max = arr[i][n-j-1]; 
            } 
        } 
    } 
    cout << "Maximum = " << max; 
         << ", Minimum = " << min; 
} 

/* Driver program to test above function */
int main() 
{ 
    int arr[MAX][MAX] = {5, 9, 11, 
                        25, 0, 14, 
                        21, 6, 4}; 
    maxMin(arr, 3); 
    return 0; 
} 

```

## Java

```java

// Java program for finding maximum  
// and minimum in a matrix. 

class GFG  
{ 
    static final int MAX = 100; 

    // Finds maximum and minimum  
    // in arr[0..n-1][0..n-1] 
    // using pair wise comparisons 
    static void maxMin(int arr[][], int n) 
    { 
        int min = +2147483647; 
        int max = -2147483648; 

        // Traverses rows one by one 
        for (int i = 0; i < n; i++) 
        { 
            for (int j = 0; j <= n/2; j++) 
            { 
                // Compare elements from beginning 
                // and end of current row 
                if (arr[i][j] > arr[i][n - j - 1]) 
                { 
                    if (min > arr[i][n - j - 1]) 
                        min = arr[i][n - j - 1]; 
                    if (max< arr[i][j]) 
                        max = arr[i][j]; 
                } 
                else
                { 
                    if (min > arr[i][j]) 
                        min = arr[i][j]; 
                    if (max< arr[i][n - j - 1]) 
                        max = arr[i][n - j - 1]; 
                } 
            } 
        } 
        System.out.print("Maximum = "+max+ 
                         ", Minimum = "+min); 
    } 

    // Driver program  
    public static void main (String[] args)  
    { 
        int arr[][] = {{5, 9, 11}, 
                       {25, 0, 14}, 
                       {21, 6, 4}}; 
        maxMin(arr, 3); 
    } 
} 

// This code is contributed by Anant Agarwal. 

```

## Python3

```py

# Python3 program for finding  
# MAXimum and MINimum in a matrix. 
MAX = 100

# Finds MAXimum and MINimum in arr[0..n-1][0..n-1] 
# using pair wise comparisons 
def MAXMIN(arr, n): 

    MIN = 10**9
    MAX = -10**9

    # Traverses rows one by one 
    for i in range(n): 
        for j in range(n // 2 + 1): 

        # Compare elements from beginning 
        # and end of current row 
            if (arr[i][j] > arr[i][n - j - 1]): 
                if (MIN > arr[i][n - j - 1]): 
                    MIN = arr[i][n - j - 1] 
                if (MAX< arr[i][j]): 
                    MAX = arr[i][j] 
            else: 
                if (MIN > arr[i][j]): 
                    MIN = arr[i][j] 
                if (MAX< arr[i][n - j - 1]): 
                    MAX = arr[i][n - j - 1] 

    print("MAXimum =", MAX, ", MINimum =", MIN) 

# Driver Code 
arr = [[5, 9, 11], 
       [25, 0, 14], 
       [21, 6, 4]] 

MAXMIN(arr, 3) 

# This code is contributed by Mohit Kumar 

```

## C# 

```cs

// C# program for finding maximum  
// and minimum in a matrix. 
using System; 

public class GFG { 

    // Finds maximum and minimum  
    // in arr[0..n-1][0..n-1] 
    // using pair wise comparisons 
    static void maxMin(int[,] arr, int n) 
    { 
        int min = +2147483647; 
        int max = -2147483648; 

        // Traverses rows one by one 
        for (int i = 0; i < n; i++) 
        { 
            for (int j = 0; j <= n/2; j++) 
            { 

                // Compare elements from beginning 
                // and end of current row 
                if (arr[i,j] > arr[i,n - j - 1]) 
                { 
                    if (min > arr[i,n - j - 1]) 
                        min = arr[i,n - j - 1]; 
                    if (max < arr[i,j]) 
                        max = arr[i,j]; 
                } 
                else
                { 
                    if (min > arr[i,j]) 
                        min = arr[i,j]; 
                    if (max < arr[i,n - j - 1]) 
                        max = arr[i,n - j - 1]; 
                } 
            } 
        } 
        Console.Write("Maximum = " + max + 
                        ", Minimum = " + min); 
    } 

    // Driver code 
    static public void Main () 
    { 
        int[,] arr = { {5, 9, 11}, 
                       {25, 0, 14}, 
                       {21, 6, 4} }; 

        maxMin(arr, 3); 
    } 
} 

// This code is contributed by Shrikant13\. 

```

## PHP

```php

<?php 
// PHP program for finding  
// maximum and minimum in 
// a matrix. 

$MAX = 100; 

// Finds maximum and minimum 
// in arr[0..n-1][0..n-1] 
// using pair wise comparisons 
function maxMin($arr, $n) 
{ 
    $min = PHP_INT_MAX; 
    $max = PHP_INT_MIN; 

    // Traverses rows one by one 
    for ($i = 0; $i < $n; $i++) 
    { 
        for ($j = 0; $j <= $n / 2; $j++) 
        { 

            // Compare elements from beginning 
            // and end of current row 
            if ($arr[$i][$j] > $arr[$i][$n - $j - 1]) 
            { 
                if ($min > $arr[$i][$n - $j - 1]) 
                    $min = $arr[$i][$n - $j - 1]; 
                if ($max< $arr[$i][$j]) 
                    $max = $arr[$i][$j]; 
            } 
            else
            { 
                if ($min > $arr[$i][$j]) 
                    $min = $arr[$i][$j]; 
                if ($max < $arr[$i][$n - $j - 1]) 
                    $max = $arr[$i][$n - $j - 1]; 
            } 
        } 
    } 
    echo "Maximum = " , $max
        ,", Minimum = " , $min; 
} 

    // Driver Code 
    $arr = array(array(5, 9, 11), 
                array(25, 0, 14), 
                array(21, 6, 4)); 
    maxMin($arr, 3); 

// This code is contributed by anuj_67\. 
?> 

```

**输出**：

```
Maximum = 25, Minimum = 0

```



