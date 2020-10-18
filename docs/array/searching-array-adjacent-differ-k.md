# 在相邻项最多相差`k`的数组中搜索

> 原文： [https://www.geeksforgeeks.org/searching-array-adjacent-differ-k/](https://www.geeksforgeeks.org/searching-array-adjacent-differ-k/)

步长数组是一个整数数组，其中每个元素与其相邻元素的差异最多为`k`。 给定键`x`，如果存在多个元素，则需要找到`x`的索引值，并返回键的首次出现。

例子：

```
Input : arr[] = {4, 5, 6, 7, 6}
           k = 1
           x = 6
Output : 2
The first index of 6 is 2.

Input : arr[] = {20, 40, 50, 70, 70, 60}  
          k = 20
          x = 60
Output : 5
The index of 60 is 5

```



此问题主要是该问题的扩展，[在相邻元素之间的差为 1 的数组中搜索元素](https://www.geeksforgeeks.org/search-an-element-in-an-array-where-difference-between-adjacent-elements-is-1/)。

**简单方法**可以一次遍历给定数组，并将每个元素与给定元素`x`进行比较。 如果匹配，则返回索引。

利用所有相邻元素之间的差异最多为`k`的事实，可以优化上述解决方案。 这个想法是从最左边的元素开始比较，并找出当前数组元素和`x`之间的差异。 将此差异设为`diff`。 从数组的给定属性中，我们始终知道`x`必须至少相距`diff / k`，因此，我们不逐一搜索，而是跳了`diff / k`。

以下是上述想法的实现。

## C++ 

```cpp

// C++ program to search an element in an array  
// where difference between all elements is 1 
#include<bits/stdc++.h> 
using namespace std; 

// x is the element to be searched in arr[0..n-1] 
// such that all elements differ by at-most k. 
int search(int arr[], int n, int x, int k) 
{ 
    // Traverse the given array starting from 
    // leftmost element 
    int i = 0; 
    while (i < n) 
    { 
        // If x is found at index i 
        if (arr[i] == x) 
            return i; 

        // Jump the difference between current 
        // array element and x divided by k 
        // We use max here to make sure that i 
        // moves at-least one step ahead. 
        i = i + max(1, abs(arr[i]-x)/k); 
    } 

    cout << "number is not present!"; 
    return -1; 
} 

// Driver program to test above function 
int main() 
{ 
    int arr[] = {2, 4, 5, 7, 7, 6}; 
    int x = 6; 
    int k = 2; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << "Element " << x  << " is present at index "
         << search(arr, n, x, k); 
    return 0; 
} 

```

## Java

```java

// Java program to search an element in  
// an array where difference between all 
// elements is 1 

import java.io.*; 

class GFG { 

    // x is the element to be searched  
    // in arr[0..n-1] such that all  
    // elements differ by at-most k. 
    static int search(int arr[], int n,  
                            int x, int k) 
    { 

        // Traverse the given array starting 
        // from leftmost element 
        int i = 0; 

        while (i < n) { 

            // If x is found at index i 
            if (arr[i] == x) 
                return i; 

            // Jump the difference between  
            // current array element and x 
            // divided by k We use max here 
            // to make sure that i moves  
            // at-least one step ahead. 
            i = i + Math.max(1, Math.abs(arr[i]  
                                      - x) / k); 
        } 

        System.out.println("number is " +  
                                "not present!"); 
        return -1; 
    } 

    // Driver program to test above function 
    public static void main(String[] args) 
    { 

        int arr[] = { 2, 4, 5, 7, 7, 6 }; 
        int x = 6; 
        int k = 2; 
        int n = arr.length; 

        System.out.println("Element " + x + 
                        " is present at index "
                        + search(arr, n, x, k)); 
    } 
} 

// This code is contributed by vt_m 

```

## Python3

```py

# Python 3 program to search an element in an array  
# where difference between all elements is 1 

# x is the element to be searched in arr[0..n-1] 
# such that all elements differ by at-most k. 
def search(arr, n, x, k): 

    # Traverse the given array starting from 
    # leftmost element 
    i = 0
    while (i < n): 

        # If x is found at index i 
        if (arr[i] == x): 
            return i 

        # Jump the difference between current 
        # array element and x divided by k 
        # We use max here to make sure that i 
        # moves at-least one step ahead. 
        i = i + max(1, int(abs(arr[i] - x) / k)) 

    print("number is not present!") 
    return -1

# Driver program to test above function 
arr = [2, 4, 5, 7, 7, 6] 
x = 6
k = 2
n = len(arr) 
print("Element", x, "is present at index",search(arr, n, x, k)) 

# This code is contributed 
# by Smitha Dinesh Semwal 

```

## C# 

```cs

// C# program to search an element in  
// an array where difference between  
// all elements is 1 
using System; 

class GFG { 

    // x is the element to be searched  
    // in arr[0..n-1] such that all  
    // elements differ by at-most k. 
    static int search(int []arr, int n,  
                          int x, int k) 
    { 

        // Traverse the given array starting 
        // from leftmost element 
        int i = 0; 

        while (i < n)  
        { 

            // If x is found at index i 
            if (arr[i] == x) 
                return i; 

            // Jump the difference between  
            // current array element and x 
            // divided by k We use max here 
            // to make sure that i moves  
            // at-least one step ahead. 
            i = i + Math.Max(1, Math.Abs(arr[i]  
                                    - x) / k); 
        } 

        Console.Write("number is " +  
                      "not present!"); 
        return -1; 
    } 

    // Driver Code 
    public static void Main() 
    { 

        int []arr = { 2, 4, 5, 7, 7, 6 }; 
        int x = 6; 
        int k = 2; 
        int n = arr.Length; 

        Console.Write("Element " + x +  
                      " is present at index " +  
                        search(arr, n, x, k)); 
    } 
} 

// This code is contributed by Nitin Mittal. 

```

## PHP

```php

<?php 
// PHP program to search an 
// element in an array where 
// difference between all  
// elements is 1 

// x is the element to be  
// searched in arr[0..n-1] 
// such that all elements  
// differ by at-most k. 
function search($arr, $n, $x, $k) 
{ 

    // Traverse the given array 
    // starting from leftmost element 
    $i = 0; 
    while ($i < $n) 
    { 
        // If x is found at index i 
        if ($arr[$i] == $x) 
            return $i; 

        // Jump the difference between current 
        // array element and x divided by k 
        // We use max here to make sure that i 
        // moves at-least one step ahead. 
        $i = $i + max(1, abs($arr[$i] - $x) / $k); 
    } 

    echo "number is not present!"; 
    return -1; 
} 

// Driver Code 
{ 
    $arr = array(2, 4, 5, 7, 7, 6); 
    $x = 6; 
    $k = 2; 
    $n = sizeof($arr)/sizeof($arr[0]); 
    echo "Element $x is present".  
                     "at index ", 
        search($arr, $n, $x, $k); 
    return 0; 
} 

// This code is contributed by nitin mittal. 
?> 

```

**输出**：

```
Element 6 is present at index 5

```



* * *

* * *



