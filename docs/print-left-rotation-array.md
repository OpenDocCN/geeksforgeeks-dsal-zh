# 在`O(n)`时间和`O(1)`空间中打印数组的左旋转

> 原文： [https://www.geeksforgeeks.org/print-left-rotation-array/](https://www.geeksforgeeks.org/print-left-rotation-array/)

给定大小为`n`的数组和多个值，我们需要围绕该值左旋转数组。 如何快速打印多个左旋？

**示例**：

```
Input : arr[] = {1, 3, 5, 7, 9}
        k1 = 1
        k2 = 3
        k3 = 4
        k4 = 6
Output : 3 5 7 9 1
         7 9 1 3 5
         9 1 3 5 7
         3 5 7 9 1

Input : arr[] = {1, 3, 5, 7, 9}
        k1 = 14 
Output : 9 1 3 5 7

```



我们在下面的文章中讨论了一个解决方案。

[快速找到数组的多个左旋转 | 系列 1](https://www.geeksforgeeks.org/quickly-find-multiple-left-rotations-of-an-array/)

上面讨论的解决方案需要额外的空间。 在本文中，我们讨论了不需要额外空间的优化解决方案。

## C++ 

```cpp

// CPP implementation of left rotation of 
// an array K number of times 
#include <bits/stdc++.h> 
using namespace std; 

// Function to leftRotate array multiple times 
void leftRotate(int arr[], int n, int k) 
{ 
    /* To get the starting point of rotated array */
    int mod = k % n; 

    // Prints the rotated array from start position 
    for (int i = 0; i < n; i++) 
        cout << (arr[(mod + i) % n]) << " "; 

    cout << "\n"; 
} 

// Driver program 
int main() 
{ 
    int arr[] = { 1, 3, 5, 7, 9 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    int k = 2; 
    leftRotate(arr, n, k); 

    k = 3; 
    leftRotate(arr, n, k); 

    k = 4; 
    leftRotate(arr, n, k); 

    return 0; 
} 

```

## Java

```java

// JAVA implementation of left rotation 
// of an array K number of times 
import java.util.*; 
import java.lang.*; 
import java.io.*; 

class arr_rot 
{    
    // Function to leftRotate array multiple 
    // times 
    static void leftRotate(int arr[], int n, 
                                     int k) 
    { 
        /* To get the starting point of  
        rotated array */
        int mod = k % n; 

        // Prints the rotated array from  
        // start position 
        for(int i = 0; i < n; ++i) 
        System.out.print(arr[(i + mod) % n] 
                          + " ");  

        System.out.println(); 
    } 

    // Driver program 
    public static void main (String[] args)  
    { 
            int arr[] = { 1, 3, 5, 7, 9 }; 
            int n = arr.length;  

            int k = 2; 
            leftRotate(arr, n, k); 

            k = 3; 
            leftRotate(arr, n, k); 

            k = 4; 
            leftRotate(arr, n, k); 
    } 
} 

// This code is contributed by Sanjal 

```

## Python

```py

# Python implementation of left rotation of 
# an array K number of times 

# Function to leftRotate array multiple times 
def leftRotate(arr, n, k): 

    # To get the starting point of rotated array 
    mod = k % n 
    s = "" 

    # Prints the rotated array from start position 
    for i in range(n): 
        print str(arr[(mod + i) % n]), 
    print
    return

# Driver program 
arr = [ 1, 3, 5, 7, 9 ] 
n = len(arr) 
k = 2
leftRotate(arr, n, k) 

k = 3
leftRotate(arr, n, k) 

k = 4
leftRotate(arr, n, k) 

#This code is contributed by Sachin Bisht 

```

## C# 

```cs

// C# implementation of left 
// rotation of an array K 
// number of times 
using System; 

class GFG 
{ 

    // Function to leftRotate  
    // array multiple times 
    static void leftRotate(int []arr,  
                           int n, int k) 
    { 
        // To get the starting   
        // point of rotated array  
        int mod = k % n; 

        // Prints the rotated array   
        // from start position 
        for(int i = 0; i < n; ++i) 
        Console.Write(arr[(i + mod) %  
                           n] + " ");  

        Console.WriteLine(); 
    } 

    // Driver Code 
    static public void Main () 
    { 
        int []arr = {1, 3, 5, 7, 9}; 
        int n = arr.Length;  

        int k = 2; 
        leftRotate(arr, n, k); 

        k = 3; 
        leftRotate(arr, n, k); 

        k = 4; 
        leftRotate(arr, n, k); 
    } 
} 

// This code is contributed by m_kit 

```

## PHP

```php

<?php 
// PHP implementation of  
// left rotation of an 
// array K number of times 

// Function to leftRotate 
// array multiple times 
function leftRotate($arr, $n, $k) 
{ 
    // To get the starting 
    // point of rotated array 
    $mod = $k % $n; 

    // Prints the rotated array 
    // from start position 
    for ($i = 0; $i < $n; $i++) 
        echo ($arr[($mod +  
                    $i) % $n]) , " "; 

    echo "\n"; 
} 

// Driver Code 
$arr = array(1, 3, 5, 7, 9); 
$n = sizeof($arr); 

$k = 2; 
leftRotate($arr, $n, $k); 

$k = 3; 
leftRotate($arr, $n, $k); 

$k = 4; 
leftRotate($arr, $n, $k); 

// This code is contributed by m_kit 
?> 

```

**输出**：

```
5 7 9 1 3 
7 9 1 3 5 
9 1 3 5 7 

```

方法二：

在下面的实现中，我们将使用标准模板库（STL），它将使解决方案更加优化和易于实现。

## C++

```cpp
// C++ Implementation For Print Left Rotation Of Any Array K
// Times
 
#include <bits/stdc++.h>
#include <iostream>
using namespace std;
// Function For The k Times Left Rotation
void leftRotate(int arr[], int k, int n)
{
 
    // Stl function rotates takes three parameters - the
    // beginning,the position by which it should be rotated
    // ,the end address of the array 
      // The below function will be rotating the array left     
    // in linear time (k%arraySize) times
    rotate(arr, arr + (k % n), arr + n);
     
      // Print the rotated array from start position
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << "\n";
}
// Driver program
int main()
{
    int arr[] = { 1, 3, 5, 7, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
   
      // Function Call
    leftRotate(arr, k, n);
 
 
    return 0;
}
```

## Java

```java
// Java implementation for print left 
// rotation of any array K times
import java.io.*;
import java.util.*;
 
class GFG{
     
// Function for the k times left rotation
static void leftRotate(Integer arr[], int k,
                                      int n)
{
   
     // In Collection class rotate function 
     // takes two parameters - the name of 
     // array and the position by which it
     // should be rotated
     // The below function will be rotating
     // the array left  in linear time
      
     // Collections.rotate()rotate the
     // array from right hence n-k
    Collections.rotate(Arrays.asList(arr), n - k); 
     
    // Print the rotated array from start position
    for(int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}
 
// Driver code
public static void main(String[] args) 
{
    Integer arr[] = { 1, 3, 5, 7, 9 };
    int n = arr.length;
    int k = 2; 
     
    // Function call
    leftRotate(arr, k, n);
}
}
 
// This code is contributed by chahattekwani71
```

输出：

```
5 7 9 1 3 
```

注意：旋转后，数组本身会更新。

