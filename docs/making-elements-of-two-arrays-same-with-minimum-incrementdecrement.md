# 使两个数组的元素相同，最小增减

> 原文： [https://www.geeksforgeeks.org/making-elements-of-two-arrays-same-with-minimum-incrementdecrement/](https://www.geeksforgeeks.org/making-elements-of-two-arrays-same-with-minimum-incrementdecrement/)

给定两个相同大小的数组，我们需要使用最少的操作将第一个数组转换为另一个数组。 在一个操作中，我们可以将元素增加或减少一个。 请注意，元素的出现顺序不必相同。

为了将一个数字转换为另一个数字，我们可以对其加减 1。

**示例**：

> 输入： `a = {3, 1, 1}`，`b = {1, 2, 2}`
> 
> 输出： 2
> 
> 说明： 在这里，我们可以通过 1 运算将任何 1 变成 2，并以一个减数运算将 3 变成 2。 因此`a[]`变成`{2, 2, 1}`，这是`b[]`的排列。
> 
> 输入： `a = {3, 1, 1}`，`b = {1, 1, 2}`
> 
> 输出： 1

**算法**：

1.首先对两个数组进行排序。

2.排序后，我们将运行一个循环，在该循环中，我们将比较第一个和第二个数组元素，并计算使第一个数组等于第二个数组所需的操作。

下面是上述方法的实现：

## C++ 

```cpp

// CPP program to find minimum increment/decrement 
// operations to make array elements same. 
#include <bits/stdc++.h> 
using namespace std; 

int MinOperation(int a[], int b[], int n) 
{ 
    // sorting both arrays in 
    // ascending order 
    sort(a, a + n); 
    sort(b, b + n); 

    // variable to store the 
    // final result 
    int result = 0; 

    // After sorting both arrays 
    // Now each array is in non- 
    // decreasing order. Thus, 
    // we will now compare each 
    // element of the array and 
    // do the increment or decrement 
    // operation depending upon the 
    // value of array b[]. 
    for (int i = 0; i < n; ++i) { 
        result = result + abs(a[i] - b[i]); 
    } 

    return result; 
} 

// Driver code 
int main() 
{ 
    int a[] = { 3, 1, 1 }; 
    int b[] = { 1, 2, 2 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    cout << MinOperation(a, b, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find minimum  
// increment/decrement operations 
// to make array elements same. 
import java.util.Arrays; 
import java.io.*; 

class GFG  
{ 
static int MinOperation(int a[], 
                        int b[],  
                        int n) 
{ 
    // sorting both arrays  
    // in ascending order 
    Arrays.sort(a); 
    Arrays.sort(b); 

    // variable to store  
    // the final result 
    int result = 0; 

    // After sorting both arrays 
    // Now each array is in non- 
    // decreasing order. Thus, 
    // we will now compare each 
    // element of the array and 
    // do the increment or decrement 
    // operation depending upon the 
    // value of array b[]. 
    for (int i = 0; i < n; ++i)  
    { 
        if (a[i] > b[i]) 
            result = result + 
                     Math.abs(a[i] - b[i]); 

        else if (a[i] < b[i]) 
            result = result +  
                     Math.abs(a[i] - b[i]); 
    } 

    return result; 
} 

// Driver code 
public static void main (String[] args)  
{ 
    int a[] = {3, 1, 1}; 
    int b[] = {1, 2, 2}; 
    int n = a.length; 
    System.out.println(MinOperation(a, b, n)); 
} 
} 

// This code is contributed 
// by akt_mit 

```

## Python3

```py

# Python 3 program to find minimum  
# increment/decrement operations to 
# make array elements same. 

def MinOperation(a, b, n): 

    # sorting both arrays in ascending order 
    a.sort(reverse = False) 
    b.sort(reverse = False) 

    # variable to store the final result 
    result = 0

    # After sorting both arrays. Now each  
    # array is in non-decreasing order.  
    # Thus, we will now compare each element 
    # of the array and do the increment or  
    # decrement operation depending upon  
    # the value of array b[]. 
    for i in range(0, n, 1): 
        if (a[i] > b[i]): 
            result = result + abs(a[i] - b[i]) 

        elif(a[i] < b[i]): 
            result = result + abs(a[i] - b[i]) 

    return result 

# Driver code 
if __name__ == '__main__': 
    a = [3, 1, 1] 
    b = [1, 2, 2] 
    n = len(a) 
    print(MinOperation(a, b, n)) 

# This code is contributed by 
# Sahil_Shelangia 

```

## C# 

```cs

//C# program to find minimum   
// increment/decrement operations  
// to make array elements same.  
using System; 
public class GFG {  

static int MinOperation(int []a,  
                        int []b,   
                        int n)  
{  
    // sorting both arrays   
    // in ascending order  
    Array.Sort(a);  
    Array.Sort(b);  

    // variable to store   
    // the final result  
    int result = 0;  

    // After sorting both arrays  
    // Now each array is in non-  
    // decreasing order. Thus,  
    // we will now compare each  
    // element of the array and  
    // do the increment or decrement  
    // operation depending upon the  
    // value of array b[].  
    for (int i = 0; i < n; ++i)   
    {  
        if (a[i] > b[i])  
            result = result +  
                     Math.Abs(a[i] - b[i]);  

        else if (a[i] < b[i])  
            result = result +   
                     Math.Abs(a[i] - b[i]);  
    }  

    return result;  
}  

// Driver code  
public static void Main ()   
{  
    int []a = {3, 1, 1};  
    int []b = {1, 2, 2};  
    int n = a.Length;  
    Console.WriteLine(MinOperation(a, b, n));  
}  
}  
/*This C# code is contributed by 29AjayKumar*/

```

## PHP

```php

<?php 
// PHP program to find minimum  
// increment/decrement operations  
// to make array elements same. 
function MinOperation($a, $b, $n) 
{ 
    // sorting both arrays in 
    // ascending order 

    sort($a); 
    sort($b); 

    // variable to store  
    // the final result 
    $result = 0; 

    // After sorting both arrays 
    // Now each array is in non- 
    // decreasing order. Thus, 
    // we will now compare each 
    // element of the array and 
    // do the increment or decrement 
    // operation depending upon the 
    // value of array b[]. 
    for ($i = 0; $i < $n; ++$i)  
    { 
        if ($a[$i] > $b[$i]) 
            $result = $result + abs($a[$i] -  
                                    $b[$i]); 

        else if ($a[$i] < $b[$i]) 
            $result = $result + abs($a[$i] -  
                                    $b[$i]); 
    } 

    return $result; 
} 

// Driver code 
$a = array ( 3, 1, 1 ); 
$b = array ( 1, 2, 2 ); 
$n = sizeof($a); 
echo MinOperation($a, $b, $n); 

// This code is contributed by ajit 
?> 

```

**输出**：

```
2

```

**时间复杂度**：`O(N log N)`。

* * *

* * *



