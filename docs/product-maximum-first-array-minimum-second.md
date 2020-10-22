# 第一个数组中的最大值与第二个数组中的最小值的乘积

> 原文： [https://www.geeksforgeeks.org/product-maximum-first-array-minimum-second/](https://www.geeksforgeeks.org/product-maximum-first-array-minimum-second/)

给定两个数组，任务是计算第一个数组的最大元素和第二个数组的最小元素的乘积。

参考文献：在 Adobe 中提问（来源：[Careercup](https://www.careercup.com/question?id=5703822780399616)）。

**示例**：

```
Input : arr1[] = {5, 7, 9, 3, 6, 2},  
        arr2[] = {1, 2, 6, -1, 0, 9} 
Output : max element in first array 
is 9 and min element in second array 
is -1\. The product of these two is -9.

Input : arr1[] = {1, 4, 2, 3, 10, 2},  
        arr2[] = {4, 2, 6, 5, 2, 9} 
Output : max element in first array 
is 10 and min element in second array 
is 2\. The product of these two is 20.

```



**方法 1 - 简单方法**：我们首先对两个数组进行排序。 然后，我们可以轻松地在第一个数组中找到最大值，在第二个数组中找到最小值。 最后，我们返回最小值和最大值的乘积。

## C++ 

```cpp

// C++ program to calculate the 
// product of max element of 
// first array and min element 
// of second array 
#include <bits/stdc++.h> 
using namespace std; 

// Function to calculate 
// the product 
int minMaxProduct(int arr1[],  
                  int arr2[],  
                  int n1,  
                  int n2) 
{ 
    // Sort the arrays to find  
    // the maximum and minimum  
    // elements in given arrays 
    sort(arr1, arr1 + n1); 
    sort(arr2, arr2 + n2); 

    // Return product of 
    // maximum and minimum. 
    return arr1[n1 - 1] * arr2[0]; 
} 

// Driven code 
int main() 
{ 
    int arr1[] = { 10, 2, 3, 6, 4, 1 }; 
    int arr2[] = { 5, 1, 4, 2, 6, 9 }; 
    int n1 = sizeof(arr1) / sizeof(arr1[0]); 
    int n2 = sizeof(arr1) / sizeof(arr1[0]); 
    cout << minMaxProductt(arr1, arr2, n1, n2); 
    return 0; 
} 

```

## Java

```java

// Java program to find the  
// to calculate the product  
// of max element of first  
// array and min element of  
// second array 
import java.util.*; 
import java.lang.*; 

class GfG 
{ 

    // Function to calculate 
    // the product 
    public static int minMaxProduct(int arr1[], 
                                    int arr2[],  
                                    int n1,  
                                    int n2) 
    { 

        // Sort the arrays to find the  
        // maximum and minimum elements  
        // in given arrays 
        Arrays.sort(arr1); 
        Arrays.sort(arr2); 

        // Return product of maximum 
        // and minimum. 
        return arr1[n1 - 1] * arr2[0]; 
    } 

    // Driver Code 
    public static void main(String argc[]) 
    { 
        int [] arr1= new int []{ 10, 2, 3,  
                                  6, 4, 1 }; 
        int [] arr2 = new int []{ 5, 1, 4,  
                                  2, 6, 9 }; 
        int n1 = 6; 
        int n2 = 6; 
        System.out.println(minMaxProduct(arr1,  
                                         arr2,  
                                         n1, n2)); 
    } 
} 

/*This code is contributed by Sagar Shukla.*/

```

## Python

```py

# A Python program to find the to 
# calculate the product of max 
# element of first array and min 
# element of second array 

# Function to calculate the product 
def minmaxProduct(arr1, arr2, n1, n2): 

    # Sort the arrays to find the  
    # maximum and minimum elements 
    # in given arrays 
    arr1.sort() 
    arr2.sort() 

    # Return product of maximum 
    # and minimum. 
    return arr1[n1 - 1] * arr2[0] 

# Driver Program 
arr1 = [10, 2, 3, 6, 4, 1] 
arr2 = [5, 1, 4, 2, 6, 9] 
n1 = len(arr1) 
n2 = len(arr2) 
print(minmaxProduct(arr1, arr2, n1, n2)) 

# This code is contributed by Shrikant13\. 

```

## C# 

```cs

// C# program to find the to  
// calculate the product of  
// max element of first array  
// and min element of second array 
using System; 

class GfG 
{ 

    // Function to calculate the product 
    public static int minMaxProduct(int []arr1,  
                                    int []arr2,  
                                    int n1,  
                                    int n2) 
    { 

        // Sort the arrays to find the  
        // maximum and minimum elements  
        // in given arrays 
        Array.Sort(arr1); 
        Array.Sort(arr2); 

        // Return product of maximum 
        // and minimum. 
        return arr1[n1 - 1] * arr2[0]; 
    } 

    // Driver Code 
    public static void Main() 
    { 
        int [] arr1= new int []{ 10, 2, 3,  
                                 6, 4, 1 }; 
        int [] arr2 = new int []{ 5, 1, 4, 
                                  2, 6, 9 }; 
        int n1 = 6; 
        int n2 = 6; 
        Console.WriteLine(minMaxProduct(arr1, arr2,  
                                        n1, n2)); 
    } 
} 

/*This code is contributed by vt_m.*/

```

## PHP

```php

<?php 
// PHP program to find the to  
// calculate the product of max 
// element of first array and 
// min element of second array 

// Function to calculate the product 
function minMaxProduct( $arr1, $arr2,  
                        $n1, $n2) 
{ 
    // Sort the arrays to find  
    // the maximum and minimum  
    // elements in given arrays 
    sort($arr1); 
    sort($arr2); 

    // Return product of 
    // maximum and minimum. 
    return $arr1[$n1 - 1] * $arr2[0]; 
} 

// Driver code 
$arr1 = array( 10, 2, 3, 6, 4, 1 ); 
$arr2 = array( 5, 1, 4, 2, 6, 9 ); 
$n1 = count($arr1); 
$n2 = count($arr2); 
echo minMaxProduct($arr1, $arr2,  
                   $n1, $n2); 

// This code is contributed by anuj_67\. 
?> 

```

**输出**：

```
10
```

**时间复杂度**：`O(N log N)`。

**空间复杂度**：`O(1)`。

**方法 2 - 高效方法**：在这种方法中，我们只需遍历整个数组，然后在第一个数组中找到最大值，在第二个数组中找到最小值，就可以轻松获得最小值和最大值的乘积。

## C++

```cpp

// C++ program to find the to  
// calculate the product of  
// max element of first array 
// and min element of second array 
#include <bits/stdc++.h> 
using namespace std; 

// Function to calculate the product 
int minMaxProduct(int arr1[], int arr2[],  
                  int n1, int n2) 
{ 
    // Initialize max of first array 
    int max = arr1[0]; 

    // initialize min of second array 
    int min = arr2[0]; 

    int i; 
    for (i = 1; i < n1 && i < n2; ++i)  
    { 

        // To find the maximum  
        // element in first array 
        if (arr1[i] > max) 
            max = arr1[i]; 

        // To find the minimum  
        // element in second array 
        if (arr2[i] < min) 
            min = arr2[i]; 
    } 

    // Process remaining elements 
    while (i < n1) 
    { 
        if (arr1[i] > max) 
        max = arr1[i];  
        i++; 
    } 
    while (i < n2) 
    { 
        if (arr2[i] < min) 
        min = arr2[i];  
        i++; 
    } 

    return max * min; 
} 

// Driven code 
int main() 
{ 
    int arr1[] = { 10, 2, 3, 6, 4, 1 }; 
    int arr2[] = { 5, 1, 4, 2, 6, 9 }; 
    int n1 = sizeof(arr1) / sizeof(arr1[0]); 
    int n2 = sizeof(arr1) / sizeof(arr1[0]); 
    cout << minMaxProduct(arr1, arr2, n1, n2) 
         << endl; 
    return 0; 
} 

```

## Java

```java
// Java program to calculate the 
// product of max element of first  
// array and min element of second array 
import java.util.*; 
import java.lang.*; 
  
class GfG 
{ 
  
    // Function to calculate the product 
    public static int minMaxProduct(int arr1[],  
                                    int arr2[],  
                                    int n1,  
                                    int n2) 
       { 
  
        // Initialize max of 
        // first array 
        int max = arr1[0]; 
  
        // initialize min of  
        // second array 
        int min = arr2[0]; 
  
        int i; 
        for (i = 1; i < n1 && i < n2; ++i)  
        { 
  
        // To find the maximum  
        // element in first array 
        if (arr1[i] > max) 
            max = arr1[i]; 
  
        // To find the minimum element 
        // in second array 
        if (arr2[i] < min) 
            min = arr2[i]; 
        } 
  
        // Process remaining elements 
        while (i < n1) 
        { 
            if (arr1[i] > max) 
            max = arr1[i];  
            i++; 
        } 
        while (i < n2) 
        { 
            if (arr2[i] < min) 
            min = arr2[i];  
            i++; 
        } 
  
        return max * min; 
    } 
      
    // Driver Code 
    public static void main(String argc[]) 
    { 
        int [] arr1= new int []{ 10, 2, 3,  
                                 6, 4, 1 }; 
        int [] arr2 = new int []{ 5, 1, 4,  
                                  2, 6, 9 }; 
        int n1 = 6; 
        int n2 = 6; 
        System.out.println(minMaxProduct(arr1, arr2,  
                                          n1, n2)); 
    } 
} 
  
// This code is contributed by Sagar Shukla
```

## Python3

```py
# Python3 program to find the to  
# calculate the product of  
# max element of first array  
# and min element of second array  
  
# Function to calculate the product  
def minMaxProduct(arr1, arr2,  
                  n1, n2) : 
  
    # Initialize max of first array  
    max = arr1[0]  
  
    # initialize min of second array  
    min = arr2[0]  
      
    i = 1
    while (i < n1 and i < n2) : 
      
        # To find the maximum  
        # element in first array  
        if (arr1[i] > max) : 
            max = arr1[i]  
  
        # To find the minimum  
        # element in second array  
        if (arr2[i] < min) : 
            min = arr2[i]  
          
        i += 1
  
    # Process remaining elements  
    while (i < n1) : 
      
        if (arr1[i] > max) : 
            max = arr1[i]  
            i += 1
      
    while (i < n2):  
      
        if (arr2[i] < min) : 
            min = arr2[i]  
            i += 1
  
    return max * min
  
# Driver code  
arr1 = [10, 2, 3, 6, 4, 1 ]  
arr2 = [5, 1, 4, 2, 6, 9 ] 
n1 = len(arr1)  
n2 = len(arr1)  
print(minMaxProduct(arr1, arr2, n1, n2)) 
  
# This code is contributed by Smitha
```

## C#

```cs
// C# program to find the to  
// calculate the product of  
// max element of first array  
// and min element of second array 
using System; 
  
class GfG 
{ 
  
    // Function to calculate 
    // the product 
    public static int minMaxProduct(int []arr1,  
                                    int []arr2,  
                                    int n1,  
                                    int n2) 
    { 
  
        // Initialize max of 
        // first array 
        int max = arr1[0]; 
  
        // initialize min of  
        // second array 
        int min = arr2[0]; 
  
        int i; 
        for (i = 1; i < n1 && i < n2; ++i)  
        { 
  
            // To find the maximum element  
            // in first array 
            if (arr1[i] > max) 
                max = arr1[i]; 
      
            // To find the minimum element 
            // in second array 
            if (arr2[i] < min) 
                min = arr2[i]; 
        } 
  
        // Process remaining elements 
        while (i < n1) 
        { 
            if (arr1[i] > max) 
            max = arr1[i];  
            i++; 
        } 
        while (i < n2) 
        { 
            if (arr2[i] < min) 
            min = arr2[i];  
            i++; 
        } 
  
        return max * min; 
    } 
      
    // Driver Code 
    public static void Main() 
    { 
        int [] arr1= new int []{ 10, 2, 3,  
                                 6, 4, 1 }; 
        int [] arr2 = new int []{ 5, 1, 4,  
                                  2, 6, 9 }; 
        int n1 = 6; 
        int n2 = 6; 
        Console.WriteLine(minMaxProduct(arr1, arr2,  
                                        n1, n2)); 
    } 
} 
  
// This code is contributed by vt_m
```

## PHP

```php
<?php 
// PHP program to find the  
// to calculate the product 
// of max element of first  
// array and min element  
// of second array 
  
// Function to calculate  
// the product 
function minMaxProduct($arr1, $arr2,  
                       $n1, $n2) 
{ 
      
    // Initialize max of 
    // first array 
    $max = $arr1[0]; 
  
    // initialize min of  
    // second array 
    $min = $arr2[0]; 
  
    $i; 
    for ($i = 1; $i < $n1 &&  
                 $i < $n2; ++$i) 
    { 
  
        // To find the maximum  
        // element in first array 
        if ($arr1[$i] > $max) 
            $max = $arr1[$i]; 
  
        // To find the minimum element 
        // in second array 
        if ($arr2[$i] < $min) 
            $min = $arr2[$i]; 
    } 
  
    // Process remaining elements 
    while ($i < $n1) 
    { 
        if ($arr1[$i] > $max) 
        $max = $arr1[$i];  
        $i++; 
    } 
    while ($i < $n2) 
    { 
        if ($arr2[$i] < $min) 
        $min = $arr2[$i];  
        $i++; 
    } 
  
    return $max * $min; 
} 
  
    // Driven code 
    $arr1 = array(10, 2, 3,  
                  6, 4, 1); 
    $arr2 = array(5, 1, 4,  
                  2, 6, 9); 
    $n1 = count($arr1); 
    $n2 = count($arr2); 
    echo minMaxProduct($arr1, $arr2,  
                       $n1, $n2); 
      
// This code is contributed by anuj_67. 
?>
```

输出：

```
10
```

时间复杂度：`O(n)`。

空间复杂度：`O(1)`。