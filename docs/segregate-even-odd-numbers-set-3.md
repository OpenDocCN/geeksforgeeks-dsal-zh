# 分离偶数和奇数 | 系列 3

> 原文： [https://www.geeksforgeeks.org/segregate-even-odd-numbers-set-3/](https://www.geeksforgeeks.org/segregate-even-odd-numbers-set-3/)

给定一个整数数组，请在该数组中分隔偶数和奇数。 所有的偶数应首先出现，然后是奇数。

例子：

```
Input : 1 9 5 3 2 6 7 11
Output : 2 6 5 3 1 9 7 11

Input : 1 3 2 4 7 6 9 10
Output : 2 4 6 10 7 1 9 3

```



我们在以下帖子中讨论了两种不同的方法：

1.  [分离偶数和奇数](https://www.geeksforgeeks.org/segregate-even-and-odd-numbers/)

2.  [分离偶数和奇数 | 系列 2](https://www.geeksforgeeks.org/segregate-even-odd-set-2/)

本文讨论的想法基于 [Lomuto 的分区方案](https://www.geeksforgeeks.org/hoares-vs-lomuto-partition-scheme-quicksort/)

1.  保持指向数组中第一个奇数元素之前位置的指针。

2.  遍历数组，如果遇到偶数，则将其与第一个奇数元素交换。

3.  继续遍历。

## C++ 

```cpp

// CPP code to segregate even odd 
// numbers in an array 
#include <bits/stdc++.h> 
using namespace std; 

// Function to segregate even odd numbers 
void arrayEvenAndOdd(int arr[], int n) 
{ 

    int i = -1, j = 0; 
    int t; 
    while (j != n) { 
        if (arr[j] % 2 == 0) { 
            i++; 

            // Swapping even and odd numbers 
            swap(arr[i], arr[j]); 
        } 
        j++; 
    } 

    // Printing segregated array 
    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 1, 3, 2, 4, 7, 6, 9, 10 }; 
    int n = sizeof(arr) / sizeof(int); 
    arrayEvenAndOdd(arr, n); 
    return 0; 
} 

```

## Java

```java

// java code to segregate even odd 
// numbers in an array 
public class GFG { 

    // Function to segregate even 
    // odd numbers 
    static void arrayEvenAndOdd( 
                  int arr[], int n) 
    { 

        int i = -1, j = 0; 
        while (j != n) { 
            if (arr[j] % 2 == 0) 
            { 
                i++; 

                // Swapping even and 
                // odd numbers 
                int temp = arr[i]; 
                arr[i] = arr[j]; 
                arr[j] = temp; 
            } 
            j++; 
        } 

        // Printing segregated array 
        for (int k = 0; k < n; k++) 
             System.out.print(arr[k] + " "); 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int arr[] = { 1, 3, 2, 4, 7,  
                            6, 9, 10 }; 
        int n = arr.length; 
        arrayEvenAndOdd(arr, n); 
    } 
} 

// This code is contributed by Sam007 

```

## Python3

```py

# Python3 code to segregate even odd  
# numbers in an array  

# Function to segregate even odd numbers  
def arrayEvenAndOdd(arr,n): 
    i = -1
    j= 0
    while (j!=n): 
        if (arr[j] % 2 ==0): 
            i = i+1

            # Swapping even and odd numbers  
            arr[i],arr[j] = arr[j],arr[i] 

        j = j+1

    # Printing segregated array  
    for i in arr: 
        print (str(i) + " " ,end='') 

# Driver Code 
if __name__=='__main__': 
    arr = [ 1 ,3, 2, 4, 7, 6, 9, 10] 
    n = len(arr) 
    arrayEvenAndOdd(arr,n) 

# This code was contributed by  
# Yatin Gupta 

```

## C# 

```cs

// C# code to segregate even odd 
// numbers in an array 
using System; 

class GFG { 

    // Function to segregate even 
    // odd numbers 
    static void arrayEvenAndOdd( 
                  int []arr, int n) 
    { 

        int i = -1, j = 0; 
        while (j != n) { 
            if (arr[j] % 2 == 0) 
            { 
                i++; 

                // Swapping even and 
                // odd numbers 
                int temp = arr[i]; 
                arr[i] = arr[j]; 
                arr[j] = temp; 
            } 
            j++; 
        } 

        // Printing segregated array 
        for (int k = 0; k < n; k++) 
            Console.Write(arr[k] + " "); 
    } 

    // Driver code     
    static void Main() 
    { 
        int []arr = { 1, 3, 2, 4, 7,  
                            6, 9, 10 }; 
        int n = arr.Length; 
        arrayEvenAndOdd(arr, n); 
    } 
} 

// This code is contributed by Sam007 

```

## PHP

```php

<?php 
// PHP code to segregate even odd 
// numbers in an array 

// Function to segregate 
// even odd numbers 
function arrayEvenAndOdd($arr, $n) 
{ 
    $i = -1; 
    $j = 0; 
    $t; 
    while ($j != $n) 
    { 
        if ($arr[$j] % 2 == 0) 
        { 
            $i++; 

            // Swapping even and 
            // odd numbers 
            $x = $arr[$i]; 
            $arr[$i] = $arr[$j]; 
            $arr[$j] = $x; 
        } 
        $j++; 
    } 

    // Printing segregated  
    // array 
    for ($i = 0; $i < $n; $i++) 
        echo $arr[$i] . " "; 
} 

    // Driver code 
    $arr = array(1, 3, 2, 4, 7, 6, 9, 10); 
    $n = sizeof($arr); 
    arrayEvenAndOdd($arr, $n); 

// This code is contributed by Anuj_67 
?> 

```

**输出**：

```
2 4 6 10 7 1 9 3

```

时间复杂度：`O(n)`。

辅助空间：`O(1)`。



* * *

* * *



