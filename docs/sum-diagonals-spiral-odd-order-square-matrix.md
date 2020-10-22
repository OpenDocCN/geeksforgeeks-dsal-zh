# 螺旋奇数阶方阵的两个对角线之和

> 原文： [https://www.geeksforgeeks.org/sum-diagonals-spiral-odd-order-square-matrix/](https://www.geeksforgeeks.org/sum-diagonals-spiral-odd-order-square-matrix/)

我们给出了一个奇数阶的螺旋矩阵，其中我们从 1 开始为中心，然后沿顺时针方向向右移动。

**示例**：

```
Input : n = 3 
Output : 25
Explanation : spiral matrix = 
7 8 9
6 1 2
5 4 3
The sum of diagonals is 7+1+3+9+5 = 25

Input : n = 5
Output : 101
Explanation : spiral matrix of order 5
21 22 23 23 25
20  7  8  9 10
19  6  1  2 11
18  5  4  3 12
17 16 15 14 13
The sum of diagonals is 21+7+1+3+13+
25+9+5+17 = 101

```



如果我们仔细看一下`n x n`的螺旋矩阵，我们会注意到右上角元素的值为`n ^ 2`。 左上角的值为`(n ^ 2) – (n - 1)`【为什么？ 并不是说我们在螺旋矩阵中逆时针移动，因此在从右上角减去`n - 1`之后，我们得到了左上角的值】。 同样，左下角的值为`(n ^ 2) – 2 (n - 1)`，右下角的值为`(n ^ 2) – 3 (n - 1)`。 在将所有四个角相加之后，我们得到`4 (n ^ 2) – 6 (n - 1)`。

令`f(n)`为`n x n`矩阵的对角元素之和。 使用上面的观察，我们可以将`f(n)`递归地写为：

```
f(n) = 4[(n^2)] – 6(n-1) + f(n-2)  
```

从上述关系式中，我们可以借助迭代法求出螺旋矩阵的所有对角元素之和。

```
spiralDiaSum(n)
{
    if (n == 1)
       return 1;

    // as order should be only odd
    // we should pass only odd-integers
    return (4*n*n - 6*n + 6 + spiralDiaSum(n-2));
}

```

下面是实现。

## C++ 

```cpp

// C++ program to find sum of 
// diagonals of spiral matrix 
#include<bits/stdc++.h> 
using namespace std; 

// function returns sum of diagonals 
int spiralDiaSum(int n) 
{ 
    if (n == 1) 
        return 1; 

    // as order should be only odd 
    // we should pass only odd-integers 
    return (4*n*n - 6*n + 6 + spiralDiaSum(n-2)); 
} 

// Driver program 
int main() 
{ 
    int n = 7; 
    cout <<  spiralDiaSum(n); 
    return 0; 
} 

```

## Java

```java
// Java program to find sum of 
// diagonals of spiral matrix 
  
class GFG  
{ 
    // function returns sum of diagonals 
    static int spiralDiaSum(int n) 
    { 
        if (n == 1) 
            return 1; 
      
        // as order should be only odd 
        // we should pass only odd-integers 
        return (4 * n * n - 6 * n + 6 +  
                     spiralDiaSum(n - 2)); 
    } 
      
    // Driver program to test 
    public static void main (String[] args)  
    { 
        int n = 7; 
        System.out.print(spiralDiaSum(n)); 
    } 
} 
  
// This code is contributed by Anant Agarwal.
```

## Python3

```py
# Python3 program to find sum of 
# diagonals of spiral matrix 
  
# function returns sum of diagonals 
def spiralDiaSum(n): 
      
    if n == 1: 
        return 1
  
    # as order should be only odd 
    # we should pass only odd 
    # integers 
    return (4 * n*n - 6 * n + 6 +
               spiralDiaSum(n-2)) 
      
# Driver program 
n = 7; 
print(spiralDiaSum(n)) 
  
# This code is contributed by Anant Agarwal.
```

## C#

```cs
// C# program to find sum of 
// diagonals of spiral matrix 
using System; 
  
class GFG  { 
      
    // function returns sum of diagonals 
    static int spiralDiaSum(int n) 
    { 
        if (n == 1) 
            return 1; 
      
        // as order should be only odd 
        // we should pass only odd-integers 
        return (4 * n * n - 6 * n + 6 +  
                spiralDiaSum(n - 2)); 
    } 
      
    // Driver code 
    public static void Main (String[] args)  
    { 
        int n = 7; 
        Console.Write(spiralDiaSum(n)); 
    } 
} 
  
// This code is contributed by parashar...
```

## PHP

```php
<?php 
// PHP program to find sum of 
// diagonals of spiral matrix 
  
// function returns sum  
// of diagonals 
function spiralDiaSum( $n) 
{ 
    if ($n == 1) 
        return 1; 
  
    // as order should be only odd 
    // we should pass only odd-integers 
    return (4 * $n * $n - 6 * $n + 6 + 
                spiralDiaSum($n - 2)); 
} 
  
// Driver Code 
$n = 7; 
echo spiralDiaSum($n); 
  
// This code is contributed by anuj_67. 
?>
```


输出：

```
261
```

