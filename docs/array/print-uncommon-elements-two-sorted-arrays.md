# 从两个排序的数组中打印不常见的元素

> 原文： [https://www.geeksforgeeks.org/print-uncommon-elements-two-sorted-arrays/](https://www.geeksforgeeks.org/print-uncommon-elements-two-sorted-arrays/)

给定两个不同元素的排序数组，我们需要从两个不常见的数组中打印那些元素。 输出应按排序顺序打印。

 **示例**：

```
Input : arr1[] = {10, 20, 30}
        arr2[] = {20, 25, 30, 40, 50}
Output : 10 25 40 50
We do not print 20 and 30 as these
elements are present in both arrays.

Input : arr1[] = {10, 20, 30}
        arr2[] = {40, 50}
Output : 10 20 30 40 50

```



这个想法基于[归并排序](http://www.geeksforgeeks.org/merge-sort/)的合并过程。 我们遍历两个数组并跳过公共元素。

## C++ 

```cpp

// C++ program to find uncommon elements of 
// two sorted arrays 
#include <bits/stdc++.h> 
using namespace std; 

void printUncommon(int arr1[], int arr2[],  
                           int n1, int n2) 
{ 

    int i = 0, j = 0, k = 0; 
    while (i < n1 && j < n2) { 

        // If not common, print smaller 
        if (arr1[i] < arr2[j]) { 
            cout << arr1[i] << " "; 
            i++; 
            k++; 
        } 
        else if (arr2[j] < arr1[i]) { 
            cout << arr2[j] << " "; 
            k++; 
            j++; 
        } 

        // Skip common element 
        else { 
            i++; 
            j++; 
        } 
    } 

    // printing remaining elements 
    while (i < n1) { 
        cout << arr1[i] << " "; 
        i++; 
        k++; 
    } 
    while (j < n2) { 
        cout << arr2[j] << " "; 
        j++; 
        k++; 
    } 
} 

// Driver code 
int main() 
{ 
    int arr1[] = {10, 20, 30}; 
    int arr2[] = {20, 25, 30, 40, 50}; 

    int n1 = sizeof(arr1) / sizeof(arr1[0]); 
    int n2 = sizeof(arr2) / sizeof(arr2[0]); 

    printUncommon(arr1, arr2, n1, n2); 

    return 0; 
} 

```

## Java

```java

// Java program to find uncommon elements 
// of two sorted arrays 
import java.io.*; 

class GFG { 

    static void printUncommon(int arr1[],  
                     int arr2[], int n1, int n2) 
    { 

        int i = 0, j = 0, k = 0; 
        while (i < n1 && j < n2) { 

            // If not common, print smaller 
            if (arr1[i] < arr2[j]) { 
                System.out.print(arr1[i] + " "); 
                i++; 
                k++; 
            } 
            else if (arr2[j] < arr1[i]) { 
                System.out.print(arr2[j] + " "); 
                k++; 
                j++; 
            } 

            // Skip common element 
            else { 
                i++; 
                j++; 
            } 
        } 

        // printing remaining elements 
        while (i < n1) { 
            System.out.print(arr1[i] + " "); 
            i++; 
            k++; 
        } 
        while (j < n2) { 
            System.out.print(arr2[j] + " "); 
            j++; 
            k++; 
        } 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int arr1[] = { 10, 20, 30 }; 
        int arr2[] = { 20, 25, 30, 40, 50 }; 

        int n1 = arr1.length; 
        int n2 = arr2.length; 

        printUncommon(arr1, arr2, n1, n2); 
    } 
} 

// This code is contributed by vt_m 

```

## Python3

```py

# Python 3 program to find uncommon 
# elements of two sorted arrays 

def printUncommon(arr1, arr2, n1, n2) : 

    i = 0
    j = 0
    k = 0
    while (i < n1 and j < n2) : 

        # If not common, print smaller 
        if (arr1[i] < arr2[j]) : 
            print( arr1[i] , end= " ") 
            i = i + 1
            k = k + 1

        elif (arr2[j] < arr1[i]) : 
            print( arr2[j] , end= " ") 
            k = k + 1
            j = j + 1

        # Skip common element 
        else : 
            i = i + 1 
            j = j + 1 

    # printing remaining elements 
    while (i < n1) : 
        print( arr1[i] , end= " ") 
        i = i + 1
        k = k + 1

    while (j < n2) : 
        print( arr2[j] , end= " ") 
        j = j + 1
        k = k + 1

# Driver code 
arr1 = [10, 20, 30] 
arr2 = [20, 25, 30, 40, 50] 

n1 = len(arr1) 
n2 = len(arr2) 

printUncommon(arr1, arr2, n1, n2) 

# This code is contributed 
# by Nikita Tiwari. 

```

## C# 

```cs

// C# program to find uncommon elements 
// of two sorted arrays 
using System; 
class GFG { 

static void printUncommon(int []arr1,  
                          int []arr2,  
                          int n1,  
                          int n2) 
    { 

        int i = 0, j = 0, k = 0; 
        while (i < n1 && j < n2) 
        { 

            // If not common, print smaller 
            if (arr1[i] < arr2[j]) 
            { 
                Console.Write(arr1[i] + " "); 
                i++; 
                k++; 
            } 
            else if (arr2[j] < arr1[i]) 
            { 
                Console.Write(arr2[j] + " "); 
                k++; 
                j++; 
            } 

            // Skip common element 
            else 
            { 
                i++; 
                j++; 
            } 
        } 

        // printing remaining elements 
        while (i < n1) 
        { 
            Console.Write(arr1[i] + " "); 
            i++; 
            k++; 
        } 
        while (j < n2)  
        { 
            Console.Write(arr2[j] + " "); 
            j++; 
            k++; 
        } 
    } 

    // Driver Code 
    public static void Main() 
    { 
        int []arr1 = {10, 20, 30}; 
        int []arr2 = {20, 25, 30, 40, 50}; 

        int n1 = arr1.Length; 
        int n2 = arr2.Length; 

        printUncommon(arr1, arr2, n1, n2); 
    } 
} 

// This code is contributed by Sam007 

```

## PHP

```php

<?php 
// PHP program to find uncommon  
// elements of two sorted arrays 

function printUncommon($arr1, $arr2,  
                       $n1, $n2) 
{ 
    $i = 0; 
    $j = 0; 
    $k = 0; 
    while ($i < $n1 && $j < $n2)  
    { 

        // If not common, prsmaller 
        if ($arr1[$i] < $arr2[$j])  
        { 
            echo $arr1[$i] . " "; 
            $i++; 
            $k++; 
        } 
        else if ($arr2[$j] < $arr1[$i])  
        { 
            echo $arr2[$j] . " "; 
            $k++; 
            $j++; 
        } 

        // Skip common element 
        else 
        { 
            $i++; 
            $j++; 
        } 
    } 

    // printing remaining elements 
    while ($i < $n1)  
    { 
        echo $arr1[$i] . " "; 
        $i++; 
        $k++; 
    } 
    while ($j < $n2)  
    { 
        echo $arr2[$j] . " "; 
        $j++; 
        $k++; 
    } 
} 

// Driver code 
$arr1 = array(10, 20, 30); 
$arr2 = array(20, 25, 30, 40, 50); 

$n1 = sizeof($arr1) ; 
$n2 = sizeof($arr2) ; 

printUncommon($arr1, $arr2, $n1, $n2); 

// This code is contributed by Anuj_67 
?> 

```

**输出**：

```
10 25 40 50

```



* * *

* * *



