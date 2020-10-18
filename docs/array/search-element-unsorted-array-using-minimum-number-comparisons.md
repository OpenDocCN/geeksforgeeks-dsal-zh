# 使用最少的比较次数搜索未排序数组中的元素

> 原文： [https://www.geeksforgeeks.org/search-element-unsorted-array-using-minimum-number-comparisons/](https://www.geeksforgeeks.org/search-element-unsorted-array-using-minimum-number-comparisons/)

给定`n`个不同整数的数组和一个元素`x`。 使用最少的比较次数在数组中搜索元素`x`。 任何种类的比较都会为比较计数贡献 1。 例如，用于终止循环的条件也将在每次执行比较时为比较计数贡献 1。 像`while(n){n--;}`这样的表达式也有助于比较计数，因为在内部对`n`的值进行了比较，从而决定是否终止循环。

例子：

```
Input : arr[] = {4, 6, 1, 5, 8}, 
        x = 1
Output : Found

Input : arr[] = {10, 3, 12, 7, 2, 11, 9}, 
        x = 15
Output : Not Found

```

在 Adobe 面试中问。



以下最简单的搜索方法在最坏的情况下需要`2n + 1`比较。

```
for (i = 0; i < n; i++)  // Worst case n+1
   if (arr[i] == x)  // Worst case n
       return i;

```

**如何减少比较次数？**

的想法是将`x`（要搜索的元素）复制到最后一个位置，以便保存`x`在`arr[]`中不存在时的最后一个比较。

**算法**：

```
search(arr, n, x)
    if arr[n-1] == x  // 1 comparison
       return "true"
    backup = arr[n-1]
    arr[n-1] = x

    for i=0, i++ // no termination condition
        if arr[i] == x // execute at most n times
                       // that is at-most n comparisons
            arr[n-1] = backup
            return (i < n-1) // 1 comparison

```

## C/C++ 

```

// C++ implementation to search an element in 
// the unsorted array using minimum number of 
// comparisons 
#include <bits/stdc++.h> 
using namespace std; 

// function to search an element in 
// minimum number of comparisons 
string search(int arr[], int n, int x) 
{ 
    // 1st comparison 
    if (arr[n - 1] == x) 
        return "Found"; 

    int backup = arr[n - 1]; 
    arr[n - 1] = x; 

    // no termination condition and thus 
    // no comparison 
    for (int i = 0;; i++) { 
        // this would be executed at-most n times 
        // and therefore at-most n comparisons 
        if (arr[i] == x) { 
            // replace arr[n-1] with its actual element 
            // as in original 'arr[]' 
            arr[n - 1] = backup; 

            // if 'x' is found before the '(n-1)th' 
            // index, then it is present in the array 
            // final comparison 
            if (i < n - 1) 
                return "Found"; 

            // else not present in the array 
            return "Not Found"; 
        } 
    } 
} 

// Driver program to test above 
int main() 
{ 
    int arr[] = { 4, 6, 1, 5, 8 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int x = 1; 
    cout << search(arr, n, x); 
    return 0; 
} 

```

## Java

```java

// Java implementation to search an element in 
// the unsorted array using minimum number of 
// comparisons 
import java.io.*; 

class GFG { 

    // Function to search an element in 
    // minimum number of comparisons 
    static String search(int arr[], int n, int x) 
    { 
        // 1st comparison 
        if (arr[n - 1] == x) 
            return "Found"; 

        int backup = arr[n - 1]; 
        arr[n - 1] = x; 

        // no termination condition and thus 
        // no comparison 
        for (int i = 0;; i++) { 
            // this would be executed at-most n times 
            // and therefore at-most n comparisons 
            if (arr[i] == x) { 
                // replace arr[n-1] with its actual element 
                // as in original 'arr[]' 
                arr[n - 1] = backup; 

                // if 'x' is found before the '(n-1)th' 
                // index, then it is present in the array 
                // final comparison 
                if (i < n - 1) 
                    return "Found"; 

                // else not present in the array 
                return "Not Found"; 
            } 
        } 
    } 

    // driver program 
    public static void main(String[] args) 
    { 
        int arr[] = { 4, 6, 1, 5, 8 }; 
        int n = arr.length; 
        int x = 1; 
        System.out.println(search(arr, n, x)); 
    } 
} 

// Contributed by Pramod Kumar 

```

## Python3

```py

# Python3 implementation to search an  
# element in the unsorted array using  
# minimum number of comparisons 

# function to search an element in 
# minimum number of comparisons 
def search(arr, n, x): 

    # 1st comparison 
    if (arr[n-1] == x) : 
        return "Found"

    backup = arr[n-1] 
    arr[n-1] = x 

    # no termination condition and  
    # thus no comparison 
    i = 0
    while(i < n) : 

        # this would be executed at-most n times 
        # and therefore at-most n comparisons 
        if (arr[i] == x) : 

            # replace arr[n-1] with its actual  
            # element as in original 'arr[]' 
            arr[n-1] = backup 

            # if 'x' is found before the '(n-1)th' 
            # index, then it is present in the  
            # array final comparison 
            if (i < n-1): 
                return "Found"

            # else not present in the array 
            return "Not Found"
        i = i + 1

# Driver Code 
arr = [4, 6, 1, 5, 8] 
n = len(arr) 
x = 1
print (search(arr, n, x)) 

# This code is contributed by rishabh_jain 

```

## C# 

```cs

// C# implementation to search an  
// element in the unsorted array  
// using minimum number of comparisons 
using System; 

class GFG { 

    // Function to search an element in 
    // minimum number of comparisons 
    static String search(int[] arr, int n, int x) 
    { 
        // 1st comparison 
        if (arr[n - 1] == x) 
            return "Found"; 

        int backup = arr[n - 1]; 
        arr[n - 1] = x; 

        // no termination condition and thus 
        // no comparison 
        for (int i = 0;; i++) { 

            // this would be executed at-most n times 
            // and therefore at-most n comparisons 
            if (arr[i] == x) { 

                // replace arr[n-1] with its actual element 
                // as in original 'arr[]' 
                arr[n - 1] = backup; 

                // if 'x' is found before the '(n-1)th' 
                // index, then it is present in the array 
                // final comparison 
                if (i < n - 1) 
                    return "Found"; 

                // else not present in the array 
                return "Not Found"; 
            } 
        } 
    } 

    // driver program 
    public static void Main() 
    { 
        int[] arr = { 4, 6, 1, 5, 8 }; 
        int n = arr.Length; 
        int x = 1; 
        Console.WriteLine(search(arr, n, x)); 
    } 
} 

// This code is contributed by Sam007 

```

## PHP

```php

<?php 
// PHP implementation to  
// search an element in 
// the unsorted array  
// using minimum number of 
// comparisons 

// function to search an 
// element in minimum 
// number of comparisons 
function search($arr, $n, $x) 
{ 

    // 1st comparison 
    if ($arr[$n - 1] == $x) 
        return "Found"; 

    $backup = $arr[$n - 1]; 
    $arr[$n - 1] = $x; 

    // no termination  
    // condition and thus 
    // no comparison 
    for ($i = 0; ; $i++) 
    { 

        // this would be executed 
        // at-most n times and 
        // therefore at-most  
        // n comparisons 
        if ($arr[$i] == $x)  
        { 

            // replace arr[n-1]  
            // with its actual element 
            // as in original 'arr[]' 
            $arr[$n - 1] = $backup; 

            // if 'x' is found before  
            // the '(n-1)th' index, 
            // then it is present  
            // in the array 
            // final comparison 
            if ($i < $n - 1) 
                return "Found"; 

            // else not present 
            // in the array 
            return "Not Found"; 
        } 
    } 
} 

// Driver Code 
$arr = array( 4, 6, 1, 5, 8 ); 
$n = sizeof($arr); 
$x = 1; 
echo(search($arr, $n, $x)); 

// This code is contributed by Ajit. 
?> 

```

Output:

```
Found

```

时间复杂度：`O(n)`。

比较数：最多`(n + 2)`比较。

