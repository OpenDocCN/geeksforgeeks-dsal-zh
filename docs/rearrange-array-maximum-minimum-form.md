# 以最大最小形式重新排列数组 | 系列 1

> 原文： [https://www.geeksforgeeks.org/rearrange-array-maximum-minimum-form/](https://www.geeksforgeeks.org/rearrange-array-maximum-minimum-form/)

给定一个带正整数的排序数组，请交替排列数组，即第一个元素应为最大值，第二个最小值，第三个第二个最大值，第四个第二个最小值等。

**示例**：

**输入**：`arr[] = {1, 2, 3, 4, 5, 6, 7}`

**输出**：`arr[] = {7, 1, 6, 2 , 5, 3, 4}`

**输入**：`arr[] = {1, 2, 3, 4, 5, 6}`

**输出**：`arr[] = {6, 1, 5, 2, 4, 3}`

预期时间复杂度：`O(n)`。



这个想法是使用一个辅助数组。 我们维护两个指针，一个指向最左或最小元素，另一个指向最右或最大元素。 我们将两个指针都指向彼此更多，或者将这些指针处的元素复制到辅助数组。 最后，我们将辅助数组复制回原始数组。

下图是上述方法的模拟：

![](img/04126d558e128ca93c1db62a8ed1dc48.png)

下面是上述方法的实现：

## C++ 

```cpp

// C++ program to rearrange an array in minimum 
// maximum form 
#include <bits/stdc++.h> 
using namespace std; 

// Prints max at first position, min at second position 
// second max at third position, second min at fourth 
// position and so on. 
void rearrange(int arr[], int n) 
{ 
    // Auxiliary array to hold modified array 
    int temp[n]; 

    // Indexes of smallest and largest elements 
    // from remaining array. 
    int small=0, large=n-1; 

    // To indicate whether we need to copy rmaining 
    // largest or remaining smallest at next position 
    int flag = true; 

    // Store result in temp[] 
    for (int i=0; i<n; i++) 
    { 
        if (flag) 
            temp[i] = arr[large--]; 
        else
            temp[i] = arr[small++]; 

        flag = !flag; 
    } 

    // Copy temp[] to arr[] 
    for (int i=0; i<n; i++) 
        arr[i] = temp[i]; 
} 

// Driver program to test above function 
int main() 
{ 
    int arr[] = {1, 2, 3, 4, 5, 6}; 
    int n = sizeof(arr)/sizeof(arr[0]); 

    cout << "Original Arrayn"; 
    for (int i=0; i<n; i++) 
        cout << arr[i] << " "; 

    rearrange(arr, n); 

    cout << "nModified Arrayn"; 
    for (int i=0; i<n; i++) 
        cout << arr[i] << " "; 
    return 0; 
} 

```

## Java

```java

// Java program to rearrange an array in minimum 
// maximum form 

import java.util.Arrays; 

public class GFG 
{ 
    // Prints max at first position, min at second position 
    // second max at third position, second min at fourth 
    // position and so on. 
    static void rearrange(int[] arr, int n) 
    { 
        // Auxiliary array to hold modified array 
        int temp[] = new int[n]; 

        // Indexes of smallest and largest elements 
        // from remaining array. 
        int small=0, large=n-1; 

        // To indicate whether we need to copy rmaining 
        // largest or remaining smallest at next position 
        boolean flag = true; 

        // Store result in temp[] 
        for (int i=0; i<n; i++) 
        { 
            if (flag) 
                temp[i] = arr[large--]; 
            else
                temp[i] = arr[small++]; 

            flag = !flag; 
        } 

        // Copy temp[] to arr[] 
        arr = temp.clone(); 
    } 

    // Driver method to test the above function 
    public static void main(String[] args)  
    { 
        int arr[] = new int[]{1, 2, 3, 4, 5, 6}; 

        System.out.println("Original Array "); 
        System.out.println(Arrays.toString(arr)); 

        rearrange(arr,arr.length); 

        System.out.println("Modified Array "); 
        System.out.println(Arrays.toString(arr)); 

    } 
} 

```

## Python

```

# Python program to rearrange an array in minimum 
# maximum form 

# Prints max at first position, min at second position 
# second max at third position, second min at fourth 
# position and so on. 
def rearrange(arr, n): 
    # Auxiliary array to hold modified array 
    temp = n*[None] 

    # Indexes of smallest and largest elements 
    # from remaining array. 
    small,large =0,n-1

    # To indicate whether we need to copy rmaining 
    # largest or remaining smallest at next position 
    flag = True

    # Store result in temp[] 
    for i in range(n): 
        if flag is True: 
            temp[i] = arr[large] 
            large -= 1
        else: 
            temp[i] = arr[small] 
            small += 1

        flag = bool(1-flag) 

    # Copy temp[] to arr[] 
    for i in range(n): 
        arr[i] = temp[i] 
    return arr 

# Driver program to test above function 
arr = [1, 2, 3, 4, 5, 6] 
n = len(arr) 
print("Original Array") 
print(arr) 
print("Modified Array") 
print(rearrange(arr, n)) 

# This code is contributed by Pratik Chhajer 

```

## C# 

```cs

// C# program to rearrange  
// an array in minimum  
// maximum form 
using System; 

class GFG 
{ 

// Prints max at first position,  
// min at second position second  
// max at third position, second  
// min at fourth position and so on. 
static void rearrage(int[] arr,  
                     int n) 
{ 
    // Auxiliary array to  
    // hold modified array 
    int []temp = new int[n]; 

    // Indexes of smallest  
    // and largest elements 
    // from remaining array. 
    int small = 0, large = n - 1; 

    // To indicate whether we  
    // need to copy rmaining 
    // largest or remaining  
    // smallest at next position 
    bool flag = true; 

    // Store result in temp[] 
    for (int i = 0; i < n; i++) 
    { 
        if (flag) 
            temp[i] = arr[large--]; 
        else
            temp[i] = arr[small++]; 

        flag = !flag; 
    } 

    // Copy temp[] to arr[] 
    for (int i = 0; i < n; i++) 
        arr[i] = temp[i]; 
} 

// Driver Code 
static void Main() 
{ 
    int[] arr = {1, 2, 3, 4,  
                 5, 6}; 

    Console.WriteLine("Original Array"); 
    for(int i = 0; i < arr.Length; i++) 
        Console.Write(arr[i] + " "); 

    rearrage(arr, arr.Length);      

    Console.WriteLine("\nModified Array"); 
    for(int i = 0; i < arr.Length; i++) 
        Console.Write(arr[i] + " "); 
} 
} 

// This code is contributed 
// by Sam007 

```

## PHP

```php

<?php 
// PHP program to rearrange an array in  
// minimum-maximum form 

// Prints max at first position, min at  
// second position second max at third  
// position, second min at fourth 
// position and so on. 
function rearrange(&$arr, $n) 
{ 
    // Auxiliary array to hold modified array 
    $temp = array(); 

    // Indexes of smallest and largest elements 
    // from remaining array. 
    $small = 0; 
    $large = $n - 1; 

    // To indicate whether we need to copy  
    // remaining largest or remaining smallest 
    // at next position 
    $flag = true; 

    // Store result in temp[] 
    for ($i = 0; $i < $n; $i++) 
    { 
        if ($flag) 
            $temp[$i] = $arr[$large--]; 
        else
            $temp[$i] = $arr[$small++]; 

        $flag = !$flag; 
    } 

    // Copy temp[] to arr[] 
    for ($i = 0; $i < $n; $i++) 
        $arr[$i] = $temp[$i]; 
} 

// Driver Code 
$arr = array(1, 2, 3, 4, 5, 6); 
$n = count($arr); 

echo "Original Arrayn\n"; 
for ($i = 0; $i < $n; $i++) 
    echo $arr[$i] . " "; 

rearrange($arr, $n); 

echo "\nModified Arrayn\n"; 
for ($i = 0; $i < $n; $i++) 
    echo $arr[$i] . " "; 

// This code is contributed by 
// Rajput-Ji 
?> 

```

**输出**：

```
Original Array
1 2 3 4 5 6
Modified Array
6 1 5 2 4 3 
```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`

**练习**：如果不允许多余的空间，如何解决此问题？

[**以最大最小形式重新排列数组 | 系列 2（`O(1)`多余的空间）**](https://www.geeksforgeeks.org/rearrange-array-maximum-minimum-form-set-2-o1-extra-space/)

