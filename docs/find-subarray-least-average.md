# 查找平均数最少的子数组

> 原文： [https://www.geeksforgeeks.org/find-subarray-least-average/](https://www.geeksforgeeks.org/find-subarray-least-average/)

给定大小为`n`的数组`arr[]`个且整数`k`，使得`k <= n`。

**示例**：

```
Input:  arr[] = {3, 7, 90, 20, 10, 50, 40}, k = 3
Output: Subarray between indexes 3 and 5
The subarray {20, 10, 50} has the least average 
among all subarrays of size 3.

Input:  arr[] = {3, 7, 5, 20, -10, 0, 12}, k = 2
Output: Subarray between [4, 5] has minimum average

```

[](https://practice.geeksforgeeks.org/problem-page.php?pid=169)

## 强烈建议您在继续解决方案之前，单击这里进行练习。

**简单解决方案**是将每个元素视为大小为`k`的子数组的开头，并计算从该元素开始的子数组的总和。 该解决方案的时间复杂度为`O(nk)`。

**有效解决方案**是要在`O(n)`时间和`O(1)`额外空间中解决上述问题。 这个想法是使用大小为`k`的滑动窗口。 跟踪当前`k`个元素的总和。 要计算当前窗口的总和，请删除上一个窗口的第一个元素，然后添加当前元素（当前窗口的最后一个元素）。

```
1) Initialize res_index = 0 // Beginning of result index
2) Find sum of first k elements. Let this sum be 'curr_sum'
3) Initialize min_sum = sum
4) Iterate from (k+1)'th to n'th element, do following
   for every element arr[i]
      a) curr_sum = curr_sum + arr[i] - arr[i-k]
      b) If curr_sum < min_sum
           res_index = (i-k+1)
5) Print res_index and res_index+k-1 as beginning and ending
   indexes of resultant subarray.
```

下面是上述算法的实现。

## C++ 

```cpp

// A Simple C++ program to find minimum average subarray 
#include <bits/stdc++.h> 
using namespace std; 

// Prints beginning and ending indexes of subarray 
// of size k with minimum average 
void findMinAvgSubarray(int arr[], int n, int k) 
{ 
    // k must be smaller than or equal to n 
    if (n < k) 
        return; 

    // Initialize  beginning index of result 
    int res_index = 0; 

    // Compute sum of first subarray of size k 
    int curr_sum = 0; 
    for (int i = 0; i < k; i++) 
        curr_sum += arr[i]; 

    // Initialize minimum sum as current sum 
    int min_sum = curr_sum; 

    // Traverse from (k+1)'th element to n'th element 
    for (int i = k; i < n; i++) { 
        // Add current item and remove first item of 
        // previous subarray 
        curr_sum += arr[i] - arr[i - k]; 

        // Update result if needed 
        if (curr_sum < min_sum) { 
            min_sum = curr_sum; 
            res_index = (i - k + 1); 
        } 
    } 

    cout << "Subarray between [" << res_index << ", "
         << res_index + k - 1 << "] has minimum average"; 
} 

// Driver program 
int main() 
{ 
    int arr[] = { 3, 7, 90, 20, 10, 50, 40 }; 
    int k = 3; // Subarray size 
    int n = sizeof arr / sizeof arr[0]; 
    findMinAvgSubarray(arr, n, k); 
    return 0; 
} 

```

## Java

```java
// A Simple Java program to find  
// minimum average subarray 
  
class Test { 
      
    static int arr[] = new int[] { 3, 7, 90, 20, 10, 50, 40 }; 
  
    // Prints beginning and ending indexes of subarray 
    // of size k with minimum average 
    static void findMinAvgSubarray(int n, int k) 
    { 
        // k must be smaller than or equal to n 
        if (n < k) 
            return; 
  
        // Initialize beginning index of result 
        int res_index = 0; 
  
        // Compute sum of first subarray of size k 
        int curr_sum = 0; 
        for (int i = 0; i < k; i++) 
            curr_sum += arr[i]; 
  
        // Initialize minimum sum as current sum 
        int min_sum = curr_sum; 
  
        // Traverse from (k+1)'th element to n'th element 
        for (int i = k; i < n; i++)  
        { 
            // Add current item and remove first 
            // item of previous subarray 
            curr_sum += arr[i] - arr[i - k]; 
  
            // Update result if needed 
            if (curr_sum < min_sum) { 
                min_sum = curr_sum; 
                res_index = (i - k + 1); 
            } 
        } 
  
        System.out.println("Subarray between [" + 
                            res_index + ", " + (res_index + k - 1) + 
                            "] has minimum average"); 
    } 
  
    // Driver method to test the above function 
    public static void main(String[] args) 
    { 
        int k = 3; // Subarray size 
        findMinAvgSubarray(arr.length, k); 
    } 
}
```

## Python3

```py
# Python3 program to find 
# minimum average subarray 
  
# Prints beginning and ending  
# indexes of subarray of size k 
# with minimum average 
def findMinAvgSubarray(arr, n, k): 
  
    # k must be smaller than or equal to n 
    if (n < k): return 0
  
    # Initialize beginning index of result 
    res_index = 0
  
    # Compute sum of first subarray of size k 
    curr_sum = 0
    for i in range(k): 
        curr_sum += arr[i] 
  
    # Initialize minimum sum as current sum 
    min_sum = curr_sum 
  
    # Traverse from (k + 1)'th 
    # element to n'th element 
    for i in range(k, n): 
      
        # Add current item and remove first  
        # item of previous subarray 
        curr_sum += arr[i] - arr[i-k] 
  
        # Update result if needed 
        if (curr_sum < min_sum): 
          
            min_sum = curr_sum 
            res_index = (i - k + 1) 
          
    print("Subarray between [", res_index, 
          ", ", (res_index + k - 1), 
          "] has minimum average") 
  
# Driver Code 
arr = [3, 7, 90, 20, 10, 50, 40] 
k = 3 # Subarray size 
n = len(arr) 
findMinAvgSubarray(arr, n, k) 
  
# This code is contributed by Anant Agarwal.
```

## C#

```cs
// A Simple C# program to find  
// minimum average subarray 
using System; 
  
class Test { 
      
    static int[] arr = new int[] { 3, 7, 90, 20, 10, 50, 40 }; 
  
    // Prints beginning and ending indexes of subarray 
    // of size k with minimum average 
    static void findMinAvgSubarray(int n, int k) 
    { 
        // k must be smaller than or equal to n 
        if (n < k) 
            return; 
  
        // Initialize beginning index of result 
        int res_index = 0; 
  
        // Compute sum of first subarray of size k 
        int curr_sum = 0; 
        for (int i = 0; i < k; i++) 
            curr_sum += arr[i]; 
  
        // Initialize minimum sum as current sum 
        int min_sum = curr_sum; 
  
        // Traverse from (k+1)'th element to n'th element 
        for (int i = k; i < n; i++)  
        { 
            // Add current item and remove first item of 
            // previous subarray 
            curr_sum += arr[i] - arr[i - k]; 
  
            // Update result if needed 
            if (curr_sum < min_sum) { 
                min_sum = curr_sum; 
                res_index = (i - k + 1); 
            } 
        } 
  
        Console.Write("Subarray between [" + res_index + ", " + 
                     (res_index + k - 1) +  
                     "] has minimum average"); 
    } 
  
    // Driver method to test the above function 
    public static void Main() 
    { 
        int k = 3; // Subarray size 
        findMinAvgSubarray(arr.Length, k); 
    } 
} 
  
// This code is contributed by nitin mittal.
```

## PHP

```php
<?php 
// A Simple PHP program to find  
// minimum average subarray 
  
// Prints beginning and ending 
// indexes of subarray of size  
// k with minimum average 
function findMinAvgSubarray($arr, $n, $k) 
{ 
      
    // k must be smaller  
    // than or equal to n 
    if ($n < $k) 
        return; 
  
    // Initialize beginning  
    // index of result 
    $res_index = 0; 
  
    // Compute sum of first 
    // subarray of size k 
    $curr_sum = 0; 
    for ($i = 0; $i < $k; $i++) 
        $curr_sum += $arr[$i]; 
  
    // Initialize minimum sum  
    // as current sum 
    $min_sum = $curr_sum; 
  
    // Traverse from (k+1)'th element 
    // to n'th element 
    for ( $i = $k; $i < $n; $i++)  
    { 
          
        // Add current item and  
        // remove first item of 
        // previous subarray 
        $curr_sum += $arr[$i] - $arr[$i - $k]; 
  
        // Update result if needed 
        if ($curr_sum < $min_sum) { 
            $min_sum = $curr_sum; 
            $res_index = ($i - $k + 1); 
        } 
    } 
  
    echo "Subarray between [" ,$res_index 
          , ", " ,$res_index + $k - 1, "] has minimum average"; 
} 
  
    // Driver Code 
    $arr = array(3, 7, 90, 20, 10, 50, 40); 
      
    // Subarray size 
    $k = 3;  
    $n = sizeof ($arr) / sizeof ($arr[0]); 
    findMinAvgSubarray($arr, $n, $k); 
    return 0; 
  
// This code is contributed by nitin mittal. 
?>
```

输出：

```
Subarray between [3, 5] has minimum average
```

时间复杂度：`O(n)`。

辅助空间：`O(1)`。