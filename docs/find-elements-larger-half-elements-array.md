# 查找大于数组中一半元素的元素

> 原文： [https://www.geeksforgeeks.org/find-elements-larger-half-elements-array/](https://www.geeksforgeeks.org/find-elements-larger-half-elements-array/)

给定`n`个元素的数组，任务是查找大于数组中元素一半的元素。 对于奇数元素，我们需要打印大于 `floor(n / 2)`个元素，其中`n`是数组中元素的总数。

**示例**：

```
Input :  arr[] = {1, 6, 3, 4}
Output : 4 6

Input  :  arr[] = {10, 4, 2, 8, 9}
Output :  10 9 8

```



**朴素的方法**是获取一个元素并将其与所有其他元素进行比较，如果大于，则增加计数，然后检查计数是否大于`n / 2`个元素，然后打印。

**有效方法**是按升序对数组进行排序，然后从排序后的数组中打印最后的`ceil(n / 2)`个元素。

下面是这种基于排序的方法的 C++ 实现。

## C/C++ 

```

// C++ program to find elements that are larger than 
// half of the elements in array 
#include <bits/stdc++.h> 
using namespace std; 

// Prints elements larger than n/2 element 
void findLarger(int arr[], int n) 
{ 
    // Sort the array in ascending order 
    sort(arr, arr + n); 

    // Print last ceil(n/2) elements 
    for (int i = n-1; i >= n/2; i--) 
        cout << arr[i] << " ";     
} 

// Driver program  
int main()  
{ 
    int arr[] = {1, 3, 6, 1, 0, 9}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    findLarger(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find elements that are  
// larger than half of the elements in array 
import java.util.*; 

class Gfg 
{ 
    // Prints elements larger than n/2 element 
    static void findLarger(int arr[], int n) 
    { 
        // Sort the array in ascending order 
        Arrays.sort(arr); 

        // Print last ceil(n/2) elements 
        for (int i = n-1; i >= n/2; i--) 
            System.out.print(arr[i] + " ");   
    } 

    // Driver program  
    public static void main(String[] args)  
    { 
        int arr[] = {1, 3, 6, 1, 0, 9}; 
        int n = arr.length; 
        findLarger(arr, n); 
    }     
} 

// This code is contributed by Raghav Sharma 

```

## Python

```py

# Python program to find elements that are larger than 
# half of the elements in array 
# Prints elements larger than n/2 element 
def findLarger(arr,n): 

    # Sort the array in ascending order 
    x = sorted(arr) 

    # Print last ceil(n/2) elements 
    for i in range(n/2,n): 
        print(x[i]), 

# Driver program 
arr = [1, 3, 6, 1, 0, 9] 
n = len(arr); 
findLarger(arr,n) 

# This code is contributed by Afzal Ansari 

```

## C# 

```cs

// C# program to find elements  
// that are larger than half  
// of the elements in array 
using System; 

class GFG 
{ 
    // Prints elements larger 
    // than n/2 element 
    static void findLarger(int []arr,  
                           int n) 
    { 
        // Sort the array  
        // in ascending order 
        Array.Sort(arr); 

        // Print last ceil(n/2) elements 
        for (int i = n - 1; i >= n / 2; i--) 
            Console.Write(arr[i] + " ");  
    } 

    // Driver Code  
    public static void Main()  
    { 
        int []arr = {1, 3, 6, 1, 0, 9}; 
        int n = arr.Length; 
        findLarger(arr, n); 
    }  
} 

// This code is contributed 
// by nitin mittal. 

```

## PHP

```php

<?php 
// PHP program to find elements 
// that are larger than half of 
// the elements in array 

// Prints elements larger 
// than n/2 element 
function findLarger($arr, $n) 
{ 
    // Sort the array in  
    // ascending order 
    sort($arr); 

    // Print last ceil(n/2) elements 
    for ($i = $n - 1; $i >= $n / 2; $i--) 
        echo $arr[$i] , " ";  
} 

// Driver Code  
$arr = array(1, 3, 6, 1, 0, 9); 
$n = count($arr); 
findLarger($arr, $n); 

// This code is contributed by anuj_67\. 
?> 

```

**输出**：

```
9 6 3

```



