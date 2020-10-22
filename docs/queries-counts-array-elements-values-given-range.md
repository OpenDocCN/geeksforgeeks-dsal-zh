# 查询值在给定范围内的数组元素的计数

> 原文： [https://www.geeksforgeeks.org/queries-counts-array-elements-values-given-range/](https://www.geeksforgeeks.org/queries-counts-array-elements-values-given-range/)

给定大小为`n`的未排序数组，请在两个元素`i`和`j`（包括两端）之间找到元素。

**示例**：

```
Input :  arr = [1 3 3 9 10 4] 
         i1 = 1, j1 = 4
         i2 = 9, j2 = 12
Output : 4
         2
The numbers are: 1 3 3 4 for first query
The numbers are: 9 10 for second query

```

**来源**： [亚马逊面试经历](https://www.geeksforgeeks.org/amazon-interview-experience-set-359-on-campus/)



**简单方法**将运行`for`循环，以检查每个元素是否在给定范围内并保持其计数。 运行每个查询的时间复杂度为`O(n)`。

## C++ 

```cpp

// Simple C++ program to count number of elements 
// with values in given range. 
#include <bits/stdc++.h> 
using namespace std; 

// function to count elements within given range 
int countInRange(int arr[], int n, int x, int y) 
{ 
    // initialize result 
    int count = 0; 
    for (int i = 0; i < n; i++) { 

        // check if element is in range 
        if (arr[i] >= x && arr[i] <= y) 
            count++; 
    } 
    return count; 
} 

// driver function 
int main() 
{ 
    int arr[] = { 1, 3, 4, 9, 10, 3 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    // Answer queries 
    int i = 1, j = 4; 
    cout << countInRange(arr, n, i, j) << endl; 

    i = 9, j = 12; 
    cout << countInRange(arr, n, i, j) << endl; 
    return 0; 
} 

```

## Java

```java

// Simple java program to count  
// number of elements with  
// values in given range. 
import java.io.*; 

class GFG  
{ 
    // function to count elements within given range 
    static int countInRange(int arr[], int n, int x, int y) 
    { 
        // initialize result 
        int count = 0; 
        for (int i = 0; i < n; i++) { 

            // check if element is in range 
            if (arr[i] >= x && arr[i] <= y) 
                count++; 
        } 
        return count; 
    } 

    // driver function 
    public static void main (String[] args) 
    { 
        int arr[] = { 1, 3, 4, 9, 10, 3 }; 
        int n = arr.length; 

        // Answer queries 
        int i = 1, j = 4; 
        System.out.println ( countInRange(arr, n, i, j)) ; 

        i = 9; 
        j = 12; 
        System.out.println ( countInRange(arr, n, i, j)) ; 

    } 
} 

// This article is contributed by vt_m 

```

## Python

```py

# function to count elements within given range 
def countInRange(arr, n, x, y): 

    # initialize result 
    count = 0; 

    for i in range(n): 

        # check if element is in range 
        if (arr[i] >= x and arr[i] <= y): 
            count += 1
    return count 

# driver function 
arr = [1, 3, 4, 9, 10, 3] 
n = len(arr) 

# Answer queries 
i = 1
j = 4
print(countInRange(arr, n, i, j)) 
i = 9
j = 12
print(countInRange(arr, n, i, j)) 

```

## C# 

```cs

// Simple C# program to count  
// number of elements with  
// values in given range. 
using System; 

class GFG  { 

    // function to count elements 
    // within given range 
    static int countInRange(int []arr, int n,  
                            int x, int y) 
    { 

        // initialize result 
        int count = 0; 
        for (int i = 0; i < n; i++) { 

            // check if element is in range 
            if (arr[i] >= x && arr[i] <= y) 
                count++; 
        } 
        return count; 
    } 

    // Driver Code 
    public static void Main () 
    { 
        int[]arr = {1, 3, 4, 9, 10, 3}; 
        int n = arr.Length; 

        // Answer queries 
        int i = 1, j = 4; 
        Console.WriteLine( countInRange(arr, n, i, j)) ; 

        i = 9; 
        j = 12; 
        Console.WriteLine( countInRange(arr, n, i, j)) ; 

    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// Simple PHP program to count 
// number of elements with  
// values in given range. 

// function to count elements 
// within given range 
function countInRange($arr, $n, 
                        $x, $y) 
{ 

    // initialize result 
    $count = 0; 
    for ($i = 0; $i < $n; $i++) 
    { 

        // check if element is in range 
        if ($arr[$i] >= $x &&  
            $arr[$i] <= $y) 
            $count++; 
    } 
    return $count; 
} 

    // Driver Code 
    $arr = array(1, 3, 4, 9, 10, 3); 
    $n = count($arr); 

    // Answer queries 
    $i = 1; 
    $j = 4; 
    echo countInRange($arr, $n, $i, $j)."\n"; 

    $i = 9; 
    $j = 12; 
    echo countInRange($arr, $n, $i, $j)."\n"; 

// This code is contributed by Sam007 
?> 

```

输出：

```
4
2

```

**有效方法**将是首先对数组进行排序，然后使用经过修改的二分搜索函数找到两个索引，第一个元素大于或等于范围下限，另一个元素小于或等于上限。 运行每个查询的时间为`O(logn)`，对数组进行一次排序的时间为`O(nlogn)`。

## C++

```cpp

// Efficient C++ program to count number of elements 
// with values in given range. 
#include <bits/stdc++.h> 
using namespace std; 

// function to find first index >= x 
int lowerIndex(int arr[], int n, int x) 
{ 
    int l = 0, h = n - 1; 
    while (l <= h) { 
        int mid = (l + h) / 2; 
        if (arr[mid] >= x) 
            h = mid - 1; 
        else
            l = mid + 1; 
    } 
    return l; 
} 

// function to find last index <= y 
int upperIndex(int arr[], int n, int y) 
{ 
    int l = 0, h = n - 1; 
    while (l <= h) { 
        int mid = (l + h) / 2; 
        if (arr[mid] <= y) 
            l = mid + 1; 
        else
            h = mid - 1; 
    } 
    return h; 
} 

// function to count elements within given range 
int countInRange(int arr[], int n, int x, int y) 
{ 
    // initialize result 
    int count = 0; 
    count = upperIndex(arr, n, y) - lowerIndex(arr, n, x) + 1; 
    return count; 
} 

// driver function 
int main() 
{ 
    int arr[] = { 1, 4, 4, 9, 10, 3 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    // Preprocess array 
    sort(arr, arr + n); 

    // Answer queries 
    int i = 1, j = 4; 
    cout << countInRange(arr, n, i, j) << endl; 

    i = 9, j = 12; 
    cout << countInRange(arr, n, i, j) << endl; 
    return 0; 
} 

```

## Java

```java

// Efficient C++ program to count number  
// of elements with values in given range. 
import java.io.*; 
import java.util.Arrays; 

class GFG  
{ 
    // function to find first index >= x 
    static int lowerIndex(int arr[], int n, int x) 
    { 
        int l = 0, h = n - 1; 
        while (l <= h)  
        { 
            int mid = (l + h) / 2; 
            if (arr[mid] >= x) 
                h = mid - 1; 
            else
                l = mid + 1; 
        } 
        return l; 
    } 

    // function to find last index <= y 
    static int upperIndex(int arr[], int n, int y) 
    { 
        int l = 0, h = n - 1; 
        while (l <= h)  
        { 
            int mid = (l + h) / 2; 
            if (arr[mid] <= y) 
                l = mid + 1; 
            else
                h = mid - 1; 
        } 
        return h; 
    } 

    // function to count elements within given range 
    static int countInRange(int arr[], int n, int x, int y) 
    { 
        // initialize result 
        int count = 0; 
        count = upperIndex(arr, n, y) -  
                lowerIndex(arr, n, x) + 1; 
        return count; 
    } 

    // Driver function 
    public static void main (String[] args)  
    { 
        int arr[] = { 1, 4, 4, 9, 10, 3 }; 
        int n = arr.length; 

        // Preprocess array 
        Arrays.sort(arr); 

        // Answer queries 
        int i = 1, j = 4; 
        System.out.println( countInRange(arr, n, i, j)); ; 

        i = 9; 
        j = 12; 
        System.out.println( countInRange(arr, n, i, j)); 

    } 
} 

// This article is contributed by vt_m. 

```

## Python

```py

# function to find first index >= x 
def lowerIndex(arr, n, x): 
  l = 0
  h = n-1
  while (l <= h): 
    mid = int((l + h)/2) 
    if (arr[mid] >= x): 
      h = mid - 1
    else: 
      l = mid + 1
  return l 

# function to find last index <= x 
def upperIndex(arr, n, x): 
  l = 0
  h = n-1
  while (l <= h): 
    mid = int((l + h)/2) 
    if (arr[mid] <= x): 
      l = mid + 1
    else: 
      h = mid - 1
  return h 

# function to count elements within given range 
def countInRange(arr, n, x, y): 
  # initialize result 
  count = 0; 
  count = upperIndex(arr, n, y) - lowerIndex(arr, n, x) + 1; 
  return count 

# driver function 
arr = [1, 3, 4, 9, 10, 3] 

# Preprocess array 
arr.sort() 
n = len(arr) 

# Answer queries 
i = 1
j = 4
print(countInRange(arr, n, i, j)) 
i = 9
j = 12
print(countInRange(arr, n, i, j)) 

```

## C#

```cs

// Efficient C# program to count number  
// of elements with values in given range. 
using System; 

class GFG  
{ 

    // function to find first index >= x 
    static int lowerIndex(int []arr, int n, 
                          int x) 
    { 

        int l = 0, h = n - 1; 
        while (l <= h)  
        { 
            int mid = (l + h) / 2; 
            if (arr[mid] >= x) 
                h = mid - 1; 
            else
                l = mid + 1; 
        } 
        return l; 
    } 

    // function to find last index <= y 
    static int upperIndex(int []arr, int n, 
                          int y) 
    { 
        int l = 0, h = n - 1; 
        while (l <= h)  
        { 
            int mid = (l + h) / 2; 
            if (arr[mid] <= y) 
                l = mid + 1; 
            else
                h = mid - 1; 
        } 
        return h; 
    } 

    // function to count elements  
    // within given range 
    static int countInRange(int []arr, int n,  
                            int x, int y) 
    { 

        // initialize result 
        int count = 0; 
        count = upperIndex(arr, n, y) -  
                lowerIndex(arr, n, x) + 1; 
        return count; 
    } 

    // Driver code 
    public static void Main ()  
    { 
        int []arr = {1, 4, 4, 9, 10, 3}; 
        int n = arr.Length; 

        // Preprocess array 
        Array.Sort(arr); 

        // Answer queries 
        int i = 1, j = 4; 
        Console.WriteLine(countInRange(arr, n, i, j)); ; 

        i = 9; 
        j = 12; 
        Console.WriteLine(countInRange(arr, n, i, j)); 

    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// Efficient PHP program to count  
// number of elements with values  
// in given range.  

// function to find first index >= x  
function lowerIndex($arr, $n, $x)  
{  
    $l = 0; $h = $n - 1;  
    while ($l <= $h) 
    {  
        $mid = ($l + $h) / 2;  
        if ($arr[$mid] >= $x)  
            $h = $mid - 1;  
        else
            $l = $mid + 1;  
    }  
    return $l;  
}  

// function to find last index <= y  
function upperIndex($arr, $n, $y)  
{  
    $l = 0; $h = $n - 1;  
    while ($l <= $h)  
    {  
        $mid = ($l + $h) / 2;  
        if ($arr[$mid] <= $y)  
            $l = $mid + 1;  
        else
            $h = $mid - 1;  
    }  
    return $h;  
}  

// function to count elements  
// within given range  
function countInRange($arr, $n, $x, $y)  
{  
    // initialize result  
    $count = 0;  
    $count = (upperIndex($arr, $n, $y) -  
              lowerIndex($arr, $n, $x) + 1); 
    $t = floor($count); 
    return $t;  
}  

// Driver Code 

$arr = array( 1, 4, 4, 9, 10, 3 );  
$n = sizeof($arr);  

// Preprocess array  
sort($arr);  

// Answer queries  
$i = 1; $j = 4;  
echo countInRange($arr, $n, $i, $j), "\n";  

$i = 9; $j = 12;  
echo countInRange($arr, $n, $i, $j), "\n";  

// This code is contributed by Sachin 
?> 

```

**输出**：

```
4
2

```

