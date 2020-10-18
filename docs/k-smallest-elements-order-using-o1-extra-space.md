# 使用`O(1)`额外空间按相同顺序排列`k`个最小元素

> 原文： [https://www.geeksforgeeks.org/k-smallest-elements-order-using-o1-extra-space/](https://www.geeksforgeeks.org/k-smallest-elements-order-using-o1-extra-space/)

您将获得一个`n`元素数组，您必须从该数组中找到`k`个最小的元素，但是它们的顺序必须与给定数组中的元素相同，并且我们只能使用`O(1)`多余的空间。

例子：

```
Input : arr[] = {4, 2, 6, 1, 5}, 
            k = 3
Output : 4 2 1
Explanation : 1, 2 and 4 are three smallest 
numbers and 4 2 1 is their order in given array

Input : arr[] = {4, 12, 16, 21, 25}, 
            k = 3
Output : 4 12 16
Explanation : 4, 12 and 16 are 3 smallest numbers
and 4 12 16 is their order in given array

```



我们已经讨论了[有效解决方案](https://www.geeksforgeeks.org/find-n-smallest-element-given-array-order-array/)，可以通过使用`O(n)`的额外空间来找到上述问题的`n`个最小元素。 为了解决这个问题而不使用任何额外的空间，我们将使用插入排序的概念。

这个想法是将`k`个最小元素以相同顺序移到开头。 为此，我们从第`k + 1`个元素开始，一直到结束。 对于每个数组元素，如果当前元素小于最大元素，则用当前元素替换前`k`个元素中的最大元素。 为了保持顺序，我们使用[插入排序](https://www.geeksforgeeks.org/insertion-sort/)的想法。

## C++ 

```cpp

// CPP for printing smallest k numbers in order 
#include <algorithm> 
#include <iostream> 
using namespace std; 

// Function to print smallest k numbers 
// in arr[0..n-1] 
void printSmall(int arr[], int n, int k) 
{ 
    // For each arr[i] find whether 
    // it is a part of n-smallest 
    // with insertion sort concept 
    for (int i = k; i < n; ++i) 
    { 
        // find largest from first k-elements 
        int max_var = arr[k-1]; 
        int pos = k-1; 
        for (int j=k-2; j>=0; j--) 
        {              
            if (arr[j] > max_var) 
            { 
                max_var = arr[j]; 
                pos = j; 
            } 
        } 

        // if largest is greater than arr[i] 
        // shift all element one place left 
        if (max_var > arr[i]) 
        { 
            int j = pos; 
            while (j < k-1) 
            { 
                arr[j] = arr[j+1]; 
                j++; 
            } 
            // make arr[k-1] = arr[i] 
            arr[k-1] = arr[i]; 
        }  
    } 
    // print result 
    for (int i=0; i<k; i++) 
        cout << arr[i] <<" "; 

} 

// Driver program 
int main() 
{ 
    int arr[] = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 }; 
    int n = sizeof(arr) / sizeof(arr[0]);  
    int k = 5; 
    printSmall(arr, n, k); 
    return 0; 
} 

```

## Java

```java

// Java for printing smallest k numbers in order 
import java.util.*; 
import java.lang.*; 

public class GfG { 
    // Function to print smallest k numbers 
    // in arr[0..n-1] 
    public static void printSmall(int arr[], int n, int k) 
    { 
        // For each arr[i] find whether 
        // it is a part of n-smallest 
        // with insertion sort concept 
        for (int i = k; i < n; ++i) { 
            // Find largest from top n-element 
            int max_var = arr[k - 1]; 
            int pos = k - 1; 
            for (int j = k - 2; j >= 0; j--) { 
                if (arr[j] > max_var) { 
                    max_var = arr[j]; 
                    pos = j; 
                } 
            } 

            // If largest is greater than arr[i] 
            // shift all element one place left 
            if (max_var > arr[i]) { 
                int j = pos; 
                while (j < k - 1) { 
                    arr[j] = arr[j + 1]; 
                    j++; 
                } 
                // make arr[k-1] = arr[i] 
                arr[k - 1] = arr[i]; 
            } 
        } 
        // print result 
        for (int i = 0; i < k; i++) 
            System.out.print(arr[i] + " "); 
    } 

    // Driver function 
    public static void main(String argc[]) 
    { 
        int[] arr = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 }; 
        int n = 10; 
        int k = 5; 
        printSmall(arr, n, k); 
    } 

} 
/* This code is contributed by Sagar Shukla */

```

## Python3

```py

# Python 3 for printing smallest 
# k numbers in order 

# Function to print smallest k  
# numbers in arr[0..n-1] 
def printSmall(arr, n, k): 

    # For each arr[i] find whether 
    # it is a part of n-smallest 
    # with insertion sort concept 
    for i in range(k, n): 

        # find largest from first k-elements 
        max_var = arr[k - 1] 
        pos = k - 1
        for j in range(k - 2, -1, -1): 

            if (arr[j] > max_var): 

                max_var = arr[j] 
                pos = j 

        # if largest is greater than arr[i] 
        # shift all element one place left 
        if (max_var > arr[i]): 

            j = pos 
            while (j < k - 1): 

                arr[j] = arr[j + 1] 
                j += 1

            # make arr[k-1] = arr[i] 
            arr[k - 1] = arr[i] 

    # print result 
    for i in range(0, k): 
        print(arr[i], end = " ") 

# Driver program 
arr = [1, 5, 8, 9, 6, 7, 3, 4, 2, 0]  
n = len(arr)  
k = 5
printSmall(arr, n, k) 

# This code is contributed by  
# Smitha Dinesh Semwal 

```

## C# 

```cs

// C# for printing smallest k numbers in order 
using System; 

public class GfG { 

    // Function to print smallest k numbers 
    // in arr[0..n-1] 
    public static void printSmall(int []arr,  
                                int n, int k) 
    { 

        // For each arr[i] find whether 
        // it is a part of n-smallest 
        // with insertion sort concept 
        for (int i = k; i < n; ++i) { 

            // Find largest from top n-element 
            int max_var = arr[k - 1]; 
            int pos = k - 1; 
            for (int j = k - 2; j >= 0; j--) 
            { 
                if (arr[j] > max_var) 
                { 
                    max_var = arr[j]; 
                    pos = j; 
                } 
            } 

            // If largest is greater than arr[i] 
            // shift all element one place left 
            if (max_var > arr[i]) { 
                int j = pos; 
                while (j < k - 1) { 
                    arr[j] = arr[j + 1]; 
                    j++; 
                } 

                // make arr[k-1] = arr[i] 
                arr[k - 1] = arr[i]; 
            } 
        } 

        // print result 
        for (int i = 0; i < k; i++) 
            Console.Write(arr[i] + " "); 
    } 

    // Driver function 
    public static void Main() 
    { 

        int[] arr = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 }; 
        int n = 10; 
        int k = 5; 

        printSmall(arr, n, k); 
    } 
} 

/* This code is contributed by Vt_m */

```

## PHP

```php

<?php 
// PHP for printing smallest  
// k numbers in order 

// Function to print smallest k  
// numbers in arr[0..n-1] 
function printSmall($arr, $n, $k) 
{ 

    // For each arr[i] find whether 
    // it is a part of n-smallest 
    // with insertion sort concept 
    for ($i = $k; $i < $n; ++$i) 
    { 

        // find largest from  
        // first k-elements 
        $max_var = $arr[$k - 1]; 
        $pos = $k - 1; 
        for ($j = $k - 2; $j >= 0; $j--) 
        {          
            if ($arr[$j] > $max_var) 
            { 
                $max_var = $arr[$j]; 
                $pos = $j; 
            } 
        } 

        // if largest is greater than arr[i] 
        // shift all element one place left 
        if ($max_var > $arr[$i]) 
        { 
            $j = $pos; 
            while ($j < $k - 1) 
            { 
                $arr[$j] = $arr[$j + 1]; 
                $j++; 
            } 

            // make arr[k - 1] = arr[i] 
            $arr[$k - 1] = $arr[$i]; 
        }  
    } 

    // print result 
    for ($i = 0; $i < $k; $i++) 
    echo $arr[$i] ," "; 

} 

    // Driver Code 
    $arr = array(1, 5, 8, 9, 6, 7, 3, 4, 2, 0); 
    $n = count($arr); 
    $k = 5; 
    printSmall($arr, $n, $k); 

// This code is contributed by Vt_m  
?> 

```

Output :

```
1 3 4 2 0

```



* * *

* * *



