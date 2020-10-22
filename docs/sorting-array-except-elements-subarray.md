# 除子数组中的元素外，对数组排序

> 原文： [https://www.geeksforgeeks.org/sorting-array-except-elements-subarray/](https://www.geeksforgeeks.org/sorting-array-except-elements-subarray/)

给定正整数数组`A`，请按升序对数组进行排序，以使未排序数组中给定子数组中的元素（输入了起始索引和结束索引）保持不动，并对所有其他元素进行排序。

**示例**：

```
Input : arr[] = {10, 4, 11, 7, 6, 20}
            l = 1, u = 3
Output : arr[] = {6, 4, 11, 7, 10, 20}
We sort elements except arr[1..3] which
is {11, 7, 6}. 

Input : arr[] = {5, 4, 3, 12, 14, 9};
            l = 1, u = 2;
Output : arr[] = {5, 4, 3, 9, 12, 14 }
We sort elements except arr[1..2] which
is {4, 3}. 

```



**方法**：将给定数组的给定限制以外的所有元素复制到另一个数组。 然后使用排序算法对另一个数组进行排序。 最后再次将排序后的数组复制到原始数组。 复制时，跳过给定的子数组。

## C++ 

```cpp

// CPP program to sort all elements except  
// given subarray. 
#include <bits/stdc++.h> 
using namespace std; 

// Sort whole array a[] except elements in 
// range a[l..r] 
void sortExceptUandL(int a[], int l, int u, int n) 
{ 
    // Copy all those element that need 
    // to be sorted to an auxiliary  
    // array b[] 
    int b[n - (u - l + 1)]; 
    for (int i = 0; i < l; i++)  
         b[i] = a[i]; 
    for (int i = u+1; i < n; i++)  
         b[l + (i - (u+1))] = a[i];     

    // sort the array b 
    sort(b, b + n - (u - l + 1)); 

    // Copy sorted elements back to a[] 
    for (int i = 0; i < l; i++)  
         a[i] = b[i]; 
    for (int i = u+1; i < n; i++)  
         a[i] = b[l + (i - (u+1))];  
} 

// Driver code 
int main() 
{ 
    int a[] = { 5, 4, 3, 12, 14, 9 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    int l = 2, u = 4; 
    sortExceptUandL(a, l, u, n); 
    for (int i = 0; i < n; i++) 
        cout << a[i] << " "; 
} 

```

## Java

```java

// Java program to sort all elements except  
// given subarray. 
import java.util.Arrays; 
import java.io.*; 

public class GFG { 

    // Sort whole array a[] except elements in 
    // range a[l..r] 
    public static void sortExceptUandL(int a[], 
                           int l, int u, int n) 
    { 

        // Copy all those element that need 
        // to be sorted to an auxiliary  
        // array b[] 
        int b[] = new int[n - (u - l + 1)]; 

        for (int i = 0; i < l; i++)  
            b[i] = a[i]; 
        for (int i = u+1; i < n; i++)  
            b[l + (i - (u+1))] = a[i];  

        // sort the array b 
        Arrays.sort(b); 

        // Copy sorted elements back to a[] 
        for (int i = 0; i < l; i++)  
            a[i] = b[i]; 
        for (int i = u+1; i < n; i++)  
            a[i] = b[l + (i - (u+1))];  
    } 
    // Driver code 
    public static void main(String args[]) 
    { 
        int a[] = { 5, 4, 3, 12, 14, 9 }; 
        int n = a.length; 
        int l = 2, u = 4; 

        sortExceptUandL(a, l, u, n); 

        for (int i = 0; i < n; i++) 
            System.out.print(a[i] + " "); 
    } 
} 

// This code is contributed by Manish Shaw 
// (manishshaw1) 

```

## Python3

```py

# Python3 program to sort all elements 
# except given subarray. 

# Sort whole array a[] except elements in 
# range a[l..r] 
def sortExceptUandL(a, l, u, n) : 

    # Copy all those element that need 
    # to be sorted to an auxiliary  
    # array b[] 
    b = [0] * (n - (u - l + 1)) 

    for i in range(0, l) : 
        b[i] = a[i] 

    for i in range(u+1, n) : 
        b[l + (i - (u+1))] = a[i]  

    # sort the array b 
    b.sort() 

    # Copy sorted elements back to a[] 
    for i in range(0, l) : 
        a[i] = b[i] 

    for i in range(u+1, n) : 
        a[i] = b[l + (i - (u+1))] 

# Driver code 
a = [ 5, 4, 3, 12, 14, 9 ] 
n = len(a) 
l = 2
u = 4
sortExceptUandL(a, l, u, n) 

for i in range(0, n) : 
    print ("{} ".format(a[i]), end="") 

# This code is contributed by 
# Manish Shaw (manishshaw1) 

```

## C# 

```cs

// C# program to sort all elements except  
// given subarray. 
using System; 
using System.Collections.Generic; 

class GFG { 

    // Sort whole array a[] except elements in 
    // range a[l..r] 
    static void sortExceptUandL(int []a, int l, 
                                 int u, int n) 
    { 

        // Copy all those element that need 
        // to be sorted to an auxiliary  
        // array b[] 
        int[] b = new int[n - (u-l+1)]; 

        for (int i = 0; i < l; i++)  
            b[i] = a[i]; 

        for (int i = u+1; i < n; i++)  
            b[l + (i - (u+1))] = a[i];  

        // sort the array b 
        Array.Sort<int>(b, 0, n - (u - l + 1)); 

        // Copy sorted elements back to a[] 
        for (int i = 0; i < l; i++)  
            a[i] = b[i]; 

        for (int i = u+1; i < n; i++)  
            a[i] = b[l + (i - (u+1))];  
    } 

    // Driver code 
    public static void Main() 
    { 
        int []a = { 5, 4, 3, 12, 14, 9 }; 
        int n = a.Length; 
        int l = 2, u = 4; 

        sortExceptUandL(a, l, u, n); 

        for (int i = 0; i < n; i++) 
            Console.Write(a[i] + " "); 
    } 
} 

// This code is contributed by Manish Shaw  
// (manishshaw1) 

```

## PHP

```php

<?php 
// PHP program to sort all  
// elements except given subarray. 

// Sort whole array a[] except 
// elements in range a[l..r] 
function sortExceptUandL($a, $l,  
                         $u, $n) 
{ 
    // Copy all those element  
    // that need to be sorted   
    // to an auxiliary array b[] 
    $b = array(); 
    for ($i = 0; $i < $l; $i++)  
        $b[$i] = $a[$i]; 
    for ($i = $u + 1; $i < $n; $i++)  
        $b[$l + ($i - ($u + 1))] = $a[$i];  

    // sort the array b 
    sort($b); 

    // Copy sorted elements 
    // back to a[] 
    for ($i = 0; $i < $l; $i++)  
        $a[$i] = $b[$i]; 
    for ($i = $u + 1; $i < $n; $i++)  
        $a[$i] = $b[$l + ($i - ($u + 1))];  
} 

// Driver code 
$a = array(4, 5, 3, 12, 14, 9); 
$n = count($a); 
$l = 2; 
$u = 4; 
sortExceptUandL($a, $l, $u, $n); 
for ($i = 0; $i < $n; $i++) 
    echo ($a[$i]. " "); 

// This code is contributed by  
// Manish Shaw(manishshaw1) 
?> 

```

**输出**：

```
4 5 3 12 14 9

```



* * *

* * *



