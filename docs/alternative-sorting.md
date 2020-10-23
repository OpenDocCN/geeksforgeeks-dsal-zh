# 替代排序

> 原文： [https://www.geeksforgeeks.org/alternative-sorting/](https://www.geeksforgeeks.org/alternative-sorting/)

给定一个整数数组，以第一个元素为最大值，第二个元素为最小值的方式打印该数组，依此类推。

**示例**：

```
Input : arr[] = {7, 1, 2, 3, 4, 5, 6}
Output : 7 1 6 2 5 3 4

Input : arr[] = {1, 6, 9, 4, 3, 7, 8, 2}
Output : 9 1 8 2 7 3 6 4

```



一个**简单解决方案**是先打印最大元素，然后再打印最小值，然后再打印第二大值，依此类推。 该方法的时间复杂度为 `O(n^2)`。

**有效解决方案**涉及以下步骤。

1.  使用`O(N log N)`算法对输入数组进行排序。

2.  我们在排序数组中维护两个指针，一个从头开始，一个从头结束。 我们也可以打印由两个指针指向的元素，并将它们彼此相对移动。

## C++ 

```cpp

// C++ program to print an array in alternate 
// sorted manner. 
#include <bits/stdc++.h> 
using namespace std; 

// Function to print alternate sorted values 
void alternateSort(int arr[], int n) 
{ 
    // Sorting the array 
    sort(arr, arr+n); 

    // Printing the last element of array  
    // first and then first element and then  
    // second last element and then second  
    // element and so on. 
    int i = 0, j = n-1; 
    while (i < j) { 
        cout << arr[j--] << " "; 
        cout << arr[i++] << " "; 
    } 

    // If the total element in array is odd  
    // then print the last middle element. 
    if (n % 2 != 0) 
        cout << arr[i]; 
} 

// Driver code 
int main() 
{ 
    int arr[] = {1, 12, 4, 6, 7, 10}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    alternateSort(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java program to print an array in alternate 
// sorted manner 
import java.io.*; 
import java.util.Arrays; 

class AlternativeString 
{ 
    // Function to print alternate sorted values 
    static void alternateSort(int arr[], int n) 
    { 
        Arrays.sort(arr); 

        // Printing the last element of array  
        // first and then first element and then  
        // second last element and then second  
        // element and so on. 
        int i = 0, j = n-1; 
        while (i < j) { 
            System.out.print(arr[j--] + " "); 
            System.out.print(arr[i++] + " "); 
        } 

        // If the total element in array is odd  
        // then print the last middle element. 
        if (n % 2 != 0) 
            System.out.print(arr[i]); 
    } 

    /* Driver program to test above functions */
    public static void main (String[] args) 
    { 
        int arr[] = {1, 12, 4, 6, 7, 10}; 
        int n = arr.length; 
        alternateSort(arr, n); 
    } 
} 
/*This code is contributed by Prakriti Gupta*/

```

## Python3

```py

# Python 3 program to print an array 
# in alternate sorted manner. 

# Function to print alternate sorted 
# values 
def alternateSort(arr, n): 

    # Sorting the array 
    arr.sort()  

    # Printing the last element of array  
    # first and then first element and then  
    # second last element and then second  
    # element and so on. 
    i = 0
    j = n-1

    while (i < j):  

        print(arr[j], end =" ") 
        j-= 1
        print(arr[i], end =" ") 
        i+= 1

    # If the total element in array is odd  
    # then print the last middle element. 
    if (n % 2 != 0): 
        print(arr[i])  

# Driver code 
arr = [1, 12, 4, 6, 7, 10]  
n = len(arr) 

alternateSort(arr, n)  

# This code is contributed by 
# Smitha Dinesh Semwal 

```

## C# 

```cs

// C# program to print an array in alternate 
// sorted manner 
using System; 

class AlternativeString { 

    // Function to print alternate sorted values 
    static void alternateSort(int[] arr, int n) 
    { 
        Array.Sort(arr); 

        // Printing the last element of array 
        // first and then first element and then 
        // second last element and then second 
        // element and so on. 
        int i = 0, j = n - 1; 
        while (i < j) { 
            Console.Write(arr[j--] + " "); 
            Console.Write(arr[i++] + " "); 
        } 

        // If the total element in array is odd 
        // then print the last middle element. 
        if (n % 2 != 0) 
            Console.WriteLine(arr[i]); 
    } 

    /* Driver program to test above functions */
    public static void Main() 
    { 
        int[] arr = { 1, 12, 4, 6, 7, 10 }; 
        int n = arr.Length; 
        alternateSort(arr, n); 
    } 
} 

// This article is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP program to print an array in  
// alternate sorted manner. 

// Function to print alternate 
// sorted values 
function alternateSort($arr, $n) 
{ 
    // Sorting the array 
    sort($arr); 

    // Printing the last element  
    // of array  first and then  
    // first element and then second  
    // last element and then second   
    // element and so on. 
    $i = 0; 
    $j = $n - 1; 
    while ($i < $j) 
    { 
        echo $arr[$j--]." "; 
        echo $arr[$i++]." "; 
    } 

    // If the total element in array   
    // is odd then print the last  
    // middle element. 
    if ($n % 2 != 0) 
        echo $arr[$i]; 
} 

// Driver code 
$arr= array(1, 12, 4, 6, 7, 10); 
$n = sizeof($arr) / sizeof($arr[0]); 

alternateSort($arr, $n); 

// This code is contributed by Mithun Kumar 
?> 

```

**输出**：

```
12 1 10 4 7 6 

```

**时间复杂度**：`O(N log N)`。

**辅助空间**：`O(1)`。

