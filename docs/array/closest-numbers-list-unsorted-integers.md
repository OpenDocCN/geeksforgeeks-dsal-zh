# 未排序整数列表中最接近的数字

> 原文： [https://www.geeksforgeeks.org/closest-numbers-list-unsorted-integers/](https://www.geeksforgeeks.org/closest-numbers-list-unsorted-integers/)

给定一列不同的未排序整数，找到它们之间的绝对差最小的那对元素？ 如果有多对，请全部找到。

例子：

```
Input : arr[] = {10, 50, 12, 100}
Output : (10, 12)
The closest elements are 10 and 12

Input : arr[] = {5, 4, 3, 2}
Output : (2, 3), (3, 4), (4, 5)

```



此问题主要是[找到任何两个元素之间的最小差异](https://www.geeksforgeeks.org/find-minimum-difference-pair/)的扩展。

1.  排序给定的数组。

2.  在排序数组中找到线性时间中所有对的最小差。

3.  再遍历排序的数组一次，以步骤 2 中获得的最小差异打印所有对。

## C++ 

```cpp

// CPP program to find minimum difference 
// an unsorted array. 
#include<bits/stdc++.h> 
using namespace std; 

// Returns minimum difference between any 
// two pair in arr[0..n-1] 
void printMinDiffPairs(int arr[], int n) 
{ 
   if (n <= 1) 
      return; 

   // Sort array elements 
   sort(arr, arr+n); 

   // Compare differences of adjacent 
   // pairs to find the minimum difference. 
   int minDiff = arr[1] - arr[0]; 
   for (int i = 2 ; i < n ; i++) 
      minDiff = min(minDiff, arr[i] - arr[i-1]); 

   // Traverse array again and print all pairs 
   // with difference as minDiff. 
   for (int i = 1; i < n; i++) 
      if ((arr[i] - arr[i-1]) == minDiff) 
         cout << "(" << arr[i-1] << ", "
              << arr[i] << "), "; 
} 

// Driver code 
int main() 
{ 
    int arr[] = {5, 3, 2, 4, 1}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    printMinDiffPairs(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find minimum  
// difference an unsorted array. 
import java.util.*; 

class GFG  
{ 

  // Returns minimum difference between  
  // any two pair in arr[0..n-1] 
  static void printMinDiffPairs(int arr[], int n) 
  { 
    if (n <= 1) 
      return; 

    // Sort array elements 
    Arrays.sort(arr); 

    // Compare differences of adjacent 
    // pairs to find the minimum difference. 
    int minDiff = arr[1] - arr[0]; 
    for (int i = 2; i < n; i++) 
      minDiff = Math.min(minDiff, arr[i] - arr[i-1]); 

    // Traverse array again and print all pairs 
    // with difference as minDiff. 
    for ( int i = 1; i < n; i++) 
     { 
        if ((arr[i] - arr[i-1]) == minDiff) 
        { 
           System.out.print("(" + arr[i-1] + ", "
                           + arr[i] + ")," ); 
        }                     
     } 
  } 

  // Driver code 
  public static void main (String[] args)  
  { 
    int arr[] = {5, 3, 2, 4, 1}; 
    int n = arr.length; 
    printMinDiffPairs(arr, n); 
  } 
} 

// This code is contributed by Ansu Kumari 

```

## Python3

```py

# Python3 program to find minimum  
# difference in an unsorted array. 

# Returns minimum difference between 
# any two pair in arr[0..n-1] 
def printMinDiffPairs(arr , n): 
    if n <= 1: return

    # Sort array elements 
    arr.sort() 

    # Compare differences of adjacent 
    # pairs to find the minimum difference. 
    minDiff = arr[1] - arr[0] 
    for i in range(2 , n): 
        minDiff = min(minDiff, arr[i] - arr[i-1]) 

    # Traverse array again and print all 
    # pairs with difference as minDiff. 
    for i in range(1 , n): 
        if (arr[i] - arr[i-1]) == minDiff: 
            print( "(" + str(arr[i-1]) + ", " 
                 + str(arr[i]) + "), ", end = '') 

# Driver code 
arr = [5, 3, 2, 4, 1] 
n = len(arr) 
printMinDiffPairs(arr , n) 

# This code is contributed by Ansu Kumari 

```

## C# 

```cs

// C# program to find minimum  
// difference an unsorted array. 
using System; 

class GFG  
{ 

// Returns minimum difference between  
// any two pair in arr[0..n-1] 
static void printMinDiffPairs(int []arr, int n) 
{ 
    if (n <= 1) 
    return; 

    // Sort array elements 
    Array.Sort(arr); 

    // Compare differences of adjacent 
    // pairs to find the minimum difference. 
    int minDiff = arr[1] - arr[0]; 
    for (int i = 2; i < n; i++) 
    minDiff = Math.Min(minDiff, arr[i] - arr[i-1]); 

    // Traverse array again and print all pairs 
    // with difference as minDiff. 
    for ( int i = 1; i < n; i++) 
    { 
        if ((arr[i] - arr[i-1]) == minDiff) 
        { 
        Console.Write(" (" + arr[i-1] + ", "
                          + arr[i] + "), " ); 
        }              
    } 
} 

// Driver code 
public static void Main ()  
{ 
    int []arr = {5, 3, 2, 4, 1}; 
    int n = arr.Length; 
    printMinDiffPairs(arr, n); 
} 
} 

// This code is contributed by vt_m 

```

## PHP

```php

<?php 
//PHP program to find minimum difference 
// an unsorted array. 

// Returns minimum difference between any 
// two pair in arr[0..n-1] 
function printMinDiffPairs($arr, $n) 
{ 
    if ($n <= 1) 
        return; 

    // Sort array elements 
    sort($arr); 

    // Compare differences of adjacent 
    // pairs to find the minimum  
    // difference. 
    $minDiff = $arr[1] - $arr[0]; 

    for ($i = 2 ; $i < $n ; $i++) 
        $minDiff = min($minDiff, $arr[$i] 
                            - $arr[$i-1]); 

    // Traverse array again and print all 
    // pairs with difference as minDiff. 
    for ($i = 1; $i < $n; $i++) 
        if (($arr[$i] - $arr[$i-1]) ==  
                                $minDiff) 
            echo "(" , $arr[$i-1] , ", ", 
                        $arr[$i] , "), "; 
} 

// Driver code 
    $arr = array(5, 3, 2, 4, 1); 
    $n = sizeof($arr); 
    printMinDiffPairs($arr, $n); 

// This code is contributed by ajit. 
?> 

```

Output:

```
(1, 2), (2, 3), (3, 4), (4, 5), 

```

**上面的程序是否处理重复项？**

上述程序未处理类似`{x, x, x}`的情况。 在这种情况下，预期输出`(x, x), (x, x), (x, x)`但在程序上方会打印`(x, x), (x, x)`。



* * *

* * *



