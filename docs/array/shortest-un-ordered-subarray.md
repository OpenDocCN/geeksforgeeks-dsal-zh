# 最短无序子数组

> 原文： [https://www.geeksforgeeks.org/shortest-un-ordered-subarray/](https://www.geeksforgeeks.org/shortest-un-ordered-subarray/)

给定一个长度为`n`的数组，问题是我们必须找到给定数组中最短的无序（既不增加也不减少）子数组的长度。

例子：

```
Input : n = 5
        7 9 10 8 11
Output : 3
Explanation : 9 10 8 unordered sub array.

Input : n = 5
       1 2 3 4 5
Output : 0 
Explanation :  Array is in increasing order.

```



这个想法基于以下事实：最短子数组的大小可以为 0 或 3。我们必须检查数组元素是增加还是减少，如果所有数组元素都在增加或减少，则最短子数组的长度为 0， 而且，如果数组元素中的任何一个都不跟随递增或递减，则其最短长度为 3。

## C++ 

```cpp

// CPP program to find shortest subarray which is 
// unsorted. 
#include <bits/stdc++.h> 
using namespace std; 

// bool function for checking an array elements  
// are in increasing. 
bool increasing(int a[], int n) 
{ 
    for (int i = 0; i < n - 1; i++)  
        if (a[i] >= a[i + 1]) 
            return false;     
    return true; 
} 

// bool function for checking an array  
// elements are in decreasing. 
bool decreasing(int a[], int n) 
{ 
    for (int i = 0; i < n - 1; i++)  
        if (a[i] < a[i + 1]) 
            return false;     
    return true; 
} 

int shortestUnsorted(int a[], int n) 
{ 
    // increasing and decreasing are two functions. 
    // if function return true value then print 
    // 0 otherwise 3\. 
    if (increasing(a, n) == true || 
       decreasing(a, n) == true) 
        return 0; 
    else
        return 3; 
} 

// Driver code 
int main() 
{ 
    int ar[] = { 7, 9, 10, 8, 11 }; 
    int n = sizeof(ar) / sizeof(ar[0]); 
    cout << shortestUnsorted(ar, n); 
    return 0; 
} 

```

## Java

```java

// JAVA program to find shortest subarray which is 
// unsorted. 
import java.util.*; 
import java.io.*; 

class GFG { 

    // boolean function to check array elements  
    // are in increasing order or not 
    public static boolean increasing(int a[],int n) 
    { 
        for (int i = 0; i < n - 1; i++)  
            if (a[i] >= a[i + 1]) 
                return false;  

        return true; 
    } 

    // boolean function to check array elements  
    // are in decreasing order or not 
    public static boolean decreasing(int arr[],int n) 
    { 
        for (int i = 0; i < n - 1; i++)  
            if (arr[i] < arr[i + 1]) 
                return false;  

        return true; 
    } 

    public static int shortestUnsorted(int a[],int n) 
    { 

        // increasing and decreasing are two functions. 
        // if function return true value then print 
        // 0 otherwise 3\. 
        if (increasing(a, n) == true ||  
                             decreasing(a, n) == true) 
            return 0; 
        else
            return 3; 
    } 

    // driver program 
    public static void main (String[] args) { 

        int ar[] = new int[]{7, 9, 10, 8, 11}; 
        int n = ar.length; 

        System.out.println(shortestUnsorted(ar,n)); 
    } 
} 

// This code is contributed by Akash Singh. 

```

## Python3

```py

# Python3 program to find shortest  
# subarray which is unsorted 

# Bool function for checking an array   
# elements are in increasing 
def increasing(a, n): 

    for i in range(0, n - 1):  
        if (a[i] >= a[i + 1]): 
            return False

    return True

# Bool function for checking an array  
# elements are in decreasing 
def decreasing(a, n): 

    for i in range(0, n - 1):  
        if (a[i] < a[i + 1]): 
            return False

    return True

def shortestUnsorted(a, n): 

    # increasing and decreasing are two functions. 
    # if function return True value then print 
    # 0 otherwise 3\. 
    if (increasing(a, n) == True or
        decreasing(a, n) == True): 
        return 0
    else: 
        return 3

# Driver code 
ar = [7, 9, 10, 8, 11]  
n = len(ar)  
print(shortestUnsorted(ar, n)) 

# This code is contributed by Smitha Dinesh Semwal.  

```

## C# 

```cs

// Program to find the shortest 
// subarray which is unsorted. 
using System; 

class GFG { 

    // boolean function to check 
    // array elements are in the 
    // increasing order or not 
    public static bool increasing(int[] a, int n) 
    { 
        for (int i = 0; i < n - 1; i++) 
            if (a[i] >= a[i + 1]) 
                return false; 

        return true; 
    } 

    // boolean function to check 
    // array elements are in the 
    // decreasing order or not 
    public static bool decreasing(int[] arr, int n) 
    { 
        for (int i = 0; i < n - 1; i++) 
            if (arr[i] < arr[i + 1]) 
                return false; 

        return true; 
    } 

    public static int shortestUnsorted(int[] a, int n) 
    { 

        // increasing and decreasing are 
        // two functions. function return 
        // true value then print 0 else 3 
         if (increasing(a, n) == true || 
             decreasing(a, n) == true) 
            return 0; 
        else
            return 3; 
    } 

    // Driver program 
    public static void Main() 
    { 

        int[] ar = new int[] { 7, 9, 10, 8, 11 }; 
        int n = ar.Length; 
        Console.WriteLine(shortestUnsorted(ar, n)); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// php program to find shortest  
// subarray which is unsorted. 

// bool function for checking an  
// array elements are in increasing. 
function increasing($a, $n) 
{ 
    for ( $i = 0; $i < $n - 1; $i++)  
        if ($a[$i] >= $a[$i + 1]) 
            return false; 

    return true; 
} 

// bool function for checking an  
// array elements are in decreasing. 
function decreasing($a, $n) 
{ 
    for ($i = 0; $i < $n - 1; $i++)  
        if ($a[$i] < $a[$i + 1]) 
            return false;  
    return true; 
} 

function shortestUnsorted($a, $n) 
{ 

    // increasing and decreasing are 
    // two functions. if function  
    // return true value then print 
    // 0 otherwise 3\. 
    if (increasing($a, $n) == true || 
          decreasing($a, $n) == true) 
        return 0; 
    else
        return 3; 
} 

// Driver code 
$ar = array( 7, 9, 10, 8, 11 ); 
$n = sizeof($ar); 
echo shortestUnsorted($ar, $n); 

// This code is contributed by 
// nitin mittal. 
?> 

```

**输出**：

```
3

```



* * *

* * *



