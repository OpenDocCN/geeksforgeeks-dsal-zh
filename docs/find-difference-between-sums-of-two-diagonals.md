# 找出两个对角线之和之间的差

> 原文： [https://www.geeksforgeeks.org/find-difference-between-sums-of-two-diagonals/](https://www.geeksforgeeks.org/find-difference-between-sums-of-two-diagonals/)

给定`n x n`的矩阵。 任务是计算对角线总和之间的绝对差。

**示例**：

```
Input : mat[][] = 11 2 4
                   4 5 6
                  10 8 -12 
Output : 15
Sum of primary diagonal = 11 + 5 + (-12) = 4.
Sum of primary diagonal = 4 + 5 + 10 = 19.
Difference = |19 - 4| = 15.

Input : mat[][] = 10 2
                   4 5
Output : 7

```



计算方阵的两个对角线的和。 沿着矩阵的第一个对角线，行索引等于列索引，即如果`i = j`，则`mat[i][j]`位于第一个对角线上。 沿着另一个对角线，`i = n – 1 – j`，即如果`i = n - 1 - j`，则`mat[i][j]`位于第二对角线上。 通过使用两个循环，我们遍历整个矩阵并计算矩阵对角线上的总和。

以下是此方法的实现：

## C++ 

```cpp

// C++ program to find the difference 
// between the sum of diagonal. 
#include <bits/stdc++.h> 
#define MAX 100 
using namespace std; 

int difference(int arr[][MAX], int n) 
{ 
    // Initialize sums of diagonals 
    int d1 = 0, d2 = 0; 

    for (int i = 0; i < n; i++) 
    { 
        for (int j = 0; j < n; j++) 
        { 
            // finding sum of primary diagonal 
            if (i == j) 
                d1 += arr[i][j]; 

            // finding sum of secondary diagonal 
            if (i == n - j - 1) 
                d2 += arr[i][j]; 
        } 
    } 

    // Absolute difference of the sums 
    // across the diagonals 
    return abs(d1 - d2); 
} 

// Driven Program 
int main() 
{ 
    int n = 3; 

    int arr[][MAX] = 
    { 
        {11, 2, 4}, 
        {4 , 5, 6}, 
        {10, 8, -12} 
    }; 

    cout << difference(arr, n); 
    return 0; 
} 

```

## Java

```java
// JAVA Code for Find difference between sums 
// of two diagonals 
class GFG { 
      
    public static int difference(int arr[][], int n) 
    { 
        // Initialize sums of diagonals 
        int d1 = 0, d2 = 0; 
       
        for (int i = 0; i < n; i++) 
        { 
            for (int j = 0; j < n; j++) 
            { 
                // finding sum of primary diagonal 
                if (i == j) 
                    d1 += arr[i][j]; 
       
                // finding sum of secondary diagonal 
                if (i == n - j - 1) 
                    d2 += arr[i][j]; 
            } 
        } 
       
        // Absolute difference of the sums 
        // across the diagonals 
        return Math.abs(d1 - d2); 
    } 
      
    /* Driver program to test above function */
    public static void main(String[] args)  
    { 
        int n = 3; 
           
        int arr[][] = 
        { 
            {11, 2, 4}, 
            {4 , 5, 6}, 
            {10, 8, -12} 
        }; 
       
        System.out.print(difference(arr, n)); 
         
    } 
  } 
// This code is contributed by Arnav Kr. Mandal.
```

## Python3

```py
# Python3 program to find the difference 
# between the sum of diagonal. 
def difference(arr, n): 
  
    # Initialize sums of diagonals 
    d1 = 0
    d2 = 0
  
    for i in range(0, n): 
      
        for j in range(0, n): 
          
            # finding sum of primary diagonal 
            if (i == j): 
                d1 += arr[i][j] 
  
            # finding sum of secondary diagonal 
            if (i == n - j - 1): 
                d2 += arr[i][j] 
          
    # Absolute difference of the sums 
    # across the diagonals 
    return abs(d1 - d2); 
  
# Driver Code 
n = 3
  
arr = [[11, 2, 4], 
       [4 , 5, 6], 
       [10, 8, -12]] 
  
print(difference(arr, n)) 
      
# This code is contributed  
# by ihritik
```

## C#

```cs
// C# Code for find difference between 
// sums of two diagonals 
using System; 
  
public class GFG 
{ 
  
    // Function to calculate difference 
    public static int difference(int[,] arr, 
                                 int n) 
    { 
          
        // Initialize sums of diagonals 
        int d1 = 0, d2 = 0; 
      
        for (int i = 0; i < n; i++) 
        { 
            for (int j = 0; j < n; j++) 
            { 
                  
                // finding sum of primary diagonal 
                if (i == j) 
                    d1 += arr[i, j]; 
      
                // finding sum of secondary diagonal 
                if (i == n - j - 1) 
                    d2 += arr[i, j]; 
            } 
        } 
      
        // Absolute difference of the 
        // sums across the diagonals 
        return Math.Abs(d1 - d2); 
    } 
      
    // Driver Code 
    public static void Main()  
    { 
        int n = 3; 
          
        int[,] arr ={{11, 2, 4}, 
                     {4 , 5, 6}, 
                     {10, 8, -12}}; 
      
        Console.Write(difference(arr, n)); 
          
    } 
} 
  
// This code is contributed by shiv_bhakt.
```

## PHP

```php
<?php 
// PHP program to find the difference 
// between the sum of diagonal. 
  
function difference($arr, $n) 
{ 
      
    // Initialize sums of diagonals 
    $d1 = 0; $d2 = 0; 
  
    for ($i = 0; $i < $n; $i++) 
    { 
        for ($j = 0; $j < $n; $j++) 
        { 
              
            // finding sum of  
            // primary diagonal 
            if ($i == $j) 
                $d1 += $arr[$i][$j]; 
  
            // finding sum of  
            // secondary diagonal 
            if ($i == $n - $j - 1) 
                $d2 += $arr[$i][$j]; 
        } 
    } 
  
    // Absolute difference of the sums 
    // across the diagonals 
    return abs($d1 - $d2); 
} 
  
// Driver Code 
{ 
    $n = 3; 
  
    $arr = array(array(11, 2, 4), 
                 array(4 , 5, 6), 
                 array(10, 8, -12)); 
  
    echo difference($arr, $n); 
    return 0; 
} 
  
// This code is contributed by nitin mittal. 
?>
```

输出：

```
15
```

时间复杂度：`O(n * n)`。

我们可以使用单元格索引中存在的模式来优化上述解决方案以在`O(n)`中工作。

## C++

```cpp
// C++ program to find the difference 
// between the sum of diagonal. 
#include <bits/stdc++.h> 
#define MAX 100 
using namespace std; 
  
int difference(int arr[][MAX], int n) 
{ 
    // Initialize sums of diagonals 
    int d1 = 0, d2 = 0; 
  
    for (int i = 0; i < n; i++) 
    { 
        d1 += arr[i][i]; 
        d2 += arr[i][n-i-1]; 
    } 
  
    // Absolute difference of the sums 
    // across the diagonals 
    return abs(d1 - d2); 
} 
  
// Driven Program 
int main() 
{ 
    int n = 3; 
  
    int arr[][MAX] = 
    { 
        {11, 2, 4}, 
        {4 , 5, 6}, 
        {10, 8, -12} 
    }; 
  
    cout << difference(arr, n); 
    return 0; 
}
```

## Java

```java
// JAVA Code for Find difference between sums 
// of two diagonals 
  
class GFG { 
      
    public static int difference(int arr[][], int n) 
    { 
        // Initialize sums of diagonals 
        int d1 = 0, d2 = 0; 
       
        for (int i = 0; i < n; i++) 
        { 
            d1 += arr[i][i]; 
            d2 += arr[i][n-i-1]; 
        } 
       
        // Absolute difference of the sums 
        // across the diagonals 
        return Math.abs(d1 - d2); 
    } 
      
    /* Driver program to test above function */
    public static void main(String[] args)  
    { 
        int n = 3; 
           
        int arr[][] = 
        { 
            {11, 2, 4}, 
            {4 , 5, 6}, 
            {10, 8, -12} 
        }; 
       
        System.out.print(difference(arr, n)); 
         
    } 
  } 
// This code is contributed by Arnav Kr. Mandal.
```

## Python3

```py
# Python3 program to find the difference 
# between the sum of diagonal. 
def difference(arr, n): 
  
    # Initialize sums of diagonals 
    d1 = 0
    d2 = 0
  
    for i in range(0, n): 
        d1 = d1 + arr[i][i] 
        d2 = d2 + arr[i][n - i - 1] 
          
    # Absolute difference of the sums 
    # across the diagonals 
    return abs(d1 - d2) 
  
# Driver Code 
n = 3
  
arr = [[11, 2, 4], 
       [4 , 5, 6], 
       [10, 8, -12]] 
  
print(difference(arr, n)) 
      
# This code is contributed 
# by ihritik
```

## C#

```cs
// C# Code for find difference between  
// sums of two diagonals 
using System; 
  
public class GFG 
  
{ 
      
    //Function to find difference 
    public static int difference(int[,] arr, 
                                 int n) 
    { 
          
        // Initialize sums of diagonals 
        int d1 = 0, d2 = 0; 
      
        for (int i = 0; i < n; i++) 
        { 
            d1 += arr[i, i]; 
            d2 += arr[i, n - i - 1]; 
        } 
      
        // Absolute difference of the sums 
        // across the diagonals 
        return Math.Abs(d1 - d2); 
    } 
      
    // Driver Code 
    public static void Main()  
    { 
        int n = 3; 
          
        int[,] arr ={{11, 2, 4}, 
                     {4 , 5, 6}, 
                     {10, 8, -12}}; 
      
        Console.Write(difference(arr, n)); 
          
    } 
} 
  
// This code is contributed by shiv_bhakt.
```

## PHP

```php
<?php 
// PHP program to find the difference 
// between the sum of diagonal. 
  
function difference($arr, $n) 
{ 
      
    // Initialize sums of diagonals 
    $d1 = 0; $d2 = 0; 
  
    for ($i = 0; $i < $n; $i++) 
    { 
        $d1 += $arr[$i][$i]; 
        $d2 += $arr[$i][$n-$i-1]; 
    } 
  
    // Absolute difference of the sums 
    // across the diagonals 
    return abs($d1 - $d2); 
} 
  
// Driver Code 
{ 
    $n = 3; 
  
    $arr =array(array(11, 2, 4), 
                array(4, 5, 6), 
                array(10, 8, -12)); 
  
    echo difference($arr, $n); 
    return 0; 
} 
  
// This code is contributed by nitin mittal. 
?>
```

输出：

```
15
```

时间复杂度：`O(n)`。