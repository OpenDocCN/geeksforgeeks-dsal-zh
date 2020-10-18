# 计算二进制矩阵中 1 和 0 的集合

> 原文： [https://www.geeksforgeeks.org/counting-sets-of-1s-and-0s-in-a-binary-matrix/](https://www.geeksforgeeks.org/counting-sets-of-1s-and-0s-in-a-binary-matrix/)

给定一个`n×m`的二进制矩阵，计算可以在行或列中形成一个或多个相同值的集合的数量。

**示例**：

```
Input: 1 0 1
       0 1 0 
Output: 8 
Explanation: There are six one-element sets
(three 1s and three 0s). There are two two-
element sets, the first one consists of the
first and the third cells of the first row.
The second one consists of the first and the 
third cells of the second row. 

Input: 1 0
       1 1 
Output: 6

```



`x`个元素的非空子集数量为` 2 ^ x –1`。我们遍历每一行并计算 1 和 0 的单元格数。 对于`u`个零和`v`个一，总集合为`2 ^ u – 1 + 2 ^ v –1`。然后遍历所有列并计算相同的值并计算总和。 我们最终从总和中减去`m x n`，因为单个元素被考虑了两次。

## CPP

```

// CPP program to compute number of sets 
// in a binary matrix. 
#include <bits/stdc++.h> 
using namespace std; 

const int m = 3; // no of columns 
const int n = 2; // no of rows 

// function to calculate the number of 
// non empty sets of cell 
long long countSets(int a[n][m]) 
{    
    // stores the final answer  
    long long res = 0; 

    // traverses row-wise  
    for (int i = 0; i < n; i++) 
    { 
        int u = 0, v = 0;  
        for (int j = 0; j < m; j++)  
            a[i][j] ? u++ : v++;           
        res += pow(2,u)-1 + pow(2,v)-1;  
    } 

    // traverses column wise  
    for (int i = 0; i < m; i++) 
    { 
        int u = 0, v = 0;  
        for (int j = 0; j < n; j++)  
             a[j][i] ? u++ : v++;   
        res += pow(2,u)-1 + pow(2,v)-1;  
    } 

    // at the end subtract n*m as no of 
    // single sets have been added twice. 
    return res-(n*m); 
} 

// driver program to test the above function. 
int main() { 

    int a[][3] = {(1, 0, 1), 
                  (0, 1, 0)}; 

    cout << countSets(a);  

    return 0; 
} 

```

## Java

```java

// Java program to compute number of sets 
// in a binary matrix. 
class GFG { 
static final int m = 3; // no of columns 
static final int n = 2; // no of rows 

// function to calculate the number of 
// non empty sets of cell 
static long countSets(int a[][]) { 

    // stores the final answer 
    long res = 0; 

    // traverses row-wise 
    for (int i = 0; i < n; i++) { 
    int u = 0, v = 0; 
    for (int j = 0; j < m; j++) { 
        if (a[i][j] == 1) 
        u++; 
        else
        v++; 
    } 
    res += Math.pow(2, u) - 1 + Math.pow(2, v) - 1; 
    } 

    // traverses column wise 
    for (int i = 0; i < m; i++) { 
    int u = 0, v = 0; 
    for (int j = 0; j < n; j++) { 
        if (a[j][i] == 1) 
        u++; 
        else
        v++; 
    } 
    res += Math.pow(2, u) - 1 + Math.pow(2, v) - 1; 
    } 

    // at the end subtract n*m as no of 
    // single sets have been added twice. 
    return res - (n * m); 
} 

// Driver code 
public static void main(String[] args) { 
    int a[][] = {{1, 0, 1}, {0, 1, 0}}; 

    System.out.print(countSets(a)); 
} 
} 
// This code is contributed by Anant Agarwal. 

```

## Python3

```py

# Python3 program to compute number of sets  
# in a binary matrix.  
m = 3 # no of columns  
n = 2 # no of rows  

# function to calculate the number of  
# non empty sets of cell  
def countSets(a): 

    # stores the final answer  
    res = 0

    # traverses row-wise  
    for i in range(n): 
        u = 0
        v = 0
        for j in range(m): 
            if a[i][j]: 
                u += 1
            else:  
                v += 1
        res += pow(2, u) - 1 + pow(2, v) - 1

    # traverses column wise  
    for i in range(m): 

        u = 0
        v = 0
        for j in range(n): 
            if a[j][i]: 
                u += 1
            else:  
                v += 1
        res += pow(2, u) - 1 + pow(2, v) - 1

    # at the end subtract n*m as no of  
    # single sets have been added twice.  
    return res - (n*m)  

# Driver program to test the above function.  
a = [[1, 0, 1],[0, 1, 0]]  

print(countSets(a)) 

# This code is conributed by shubhamsingh10 

```

## C# 

```cs

// C# program to compute number of 
// sets in a binary matrix. 
using System; 

class GFG { 

    static int m = 3; // no of columns 
    static int n = 2; // no of rows 

    // function to calculate the number of 
    // non empty sets of cell 
    static long countSets(int [,]a) 
    { 

        // stores the final answer 
        long res = 0; 

        // Traverses row-wise 
        for (int i = 0; i < n; i++) 
        { 
            int u = 0, v = 0; 

            for (int j = 0; j < m; j++) 
            { 
                if (a[i,j] == 1) 
                    u++; 
                else
                    v++; 
            } 
            res += (long)(Math.Pow(2, u) - 1 
                       + Math.Pow(2, v)) - 1; 
        } 

        // Traverses column wise 
        for (int i = 0; i < m; i++) 
        { 
            int u = 0, v = 0; 

            for (int j = 0; j < n; j++) 
            { 
                if (a[j,i] == 1) 
                    u++; 
                else
                    v++; 
            } 
            res += (long)(Math.Pow(2, u) - 1 
                       + Math.Pow(2, v)) - 1; 
        } 

        // at the end subtract n*m as no of 
        // single sets have been added twice. 
        return res - (n * m); 
    } 

    // Driver code 
    public static void Main() 
    { 
        int [,]a = {{1, 0, 1}, {0, 1, 0}}; 

        Console.WriteLine(countSets(a)); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP program to compute 
// number of sets 
// in a binary matrix. 

// no of columns 
$m = 3;  

// no of rows 
$n = 2;  

// function to calculate the number  
// of non empty sets of cell 
function countSets($a) 
{  
    global $m, $n; 

    // stores the final answer  
    $res = 0; 

    // traverses row-wise  
    for ($i = 0; $i < $n; $i++) 
    { 
        $u = 0; $v = 0;  
        for ( $j = 0; $j < $m; $j++)  
            $a[$i][$j] ? $u++ : $v++;      
        $res += pow(2, $u) - 1 + pow(2, $v) - 1;  
    }  

    // traverses column wise  
    for ($i = 0; $i < $m; $i++) 
    { 
        $u = 0;$v = 0;  
        for ($j = 0; $j < $n; $j++)  
            $a[$j][$i] ? $u++ : $v++;  
        $res += pow(2, $u) - 1 +  
                pow(2, $v) - 1;  
    } 

    // at the end subtract 
    // n*m as no of single 
    // sets have been added  
    // twice. 
    return $res-($n*$m); 
} 

    // Driver Code 
    $a = array(array(1, 0, 1), 
               array(0, 1, 0)); 

    echo countSets($a);  

// This code is contributed by anuj_67\. 
?> 

```

Output:

```
8

```

时间复杂度：`O(n * m)`。



