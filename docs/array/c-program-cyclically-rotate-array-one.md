# 循环旋转数组的程序

> 原文： [https://www.geeksforgeeks.org/c-program-cyclically-rotate-array-one/](https://www.geeksforgeeks.org/c-program-cyclically-rotate-array-one/)

给定一个数组，将数组顺时针方向顺时针旋转一个。

**示例**：

```
Input:  arr[] = {1, 2, 3, 4, 5}
Output: arr[] = {5, 1, 2, 3, 4}

```



以下是步骤。

1.  将最后一个元素存储在变量`x`中。

2.  将所有元素向前移动一个位置。

3.  将数组的第一个元素替换为`x`。

## C++ 

```cpp

// C++ code for program  
// to cyclically rotate 
// an array by one 
# include <iostream> 
using namespace std; 

void rotate(int arr[], int n) 
{ 
    int x = arr[n - 1], i; 
    for (i = n - 1; i > 0; i--) 
    arr[i] = arr[i - 1];  
    arr[0] = x; 
} 

// Driver code 
int main()  
{ 
    int arr[] = {1, 2, 3, 4, 5}, i; 
    int n = sizeof(arr) /  
            sizeof(arr[0]); 

    cout << "Given array is \n"; 
    for (i = 0; i < n; i++) 
        cout << arr[i]; 

    rotate(arr, n); 

    cout << "\nRotated array is\n"; 
    for (i = 0; i < n; i++) 
        cout << arr[i]; 

    return 0; 
} 

// This code is contributed by jit_t 

```

## C

```c

#include <stdio.h> 

void rotate(int arr[], int n) 
{ 
   int x = arr[n-1], i; 
   for (i = n-1; i > 0; i--) 
      arr[i] = arr[i-1]; 
   arr[0] = x; 
} 

int main() 
{ 
    int arr[] = {1, 2, 3, 4, 5}, i; 
    int n = sizeof(arr)/sizeof(arr[0]); 

    printf("Given array is\n"); 
    for (i = 0; i < n; i++) 
        printf("%d ", arr[i]); 

    rotate(arr, n); 

    printf("\nRotated array is\n"); 
    for (i = 0; i < n; i++) 
        printf("%d ", arr[i]); 

    return 0; 
}

```

## Java

```java

import java.util.Arrays; 

public class Test 
{ 
    static int arr[] = new int[]{1, 2, 3, 4, 5}; 

    // Method for rotation 
    static void rotate() 
    { 
       int x = arr[arr.length-1], i; 
       for (i = arr.length-1; i > 0; i--) 
          arr[i] = arr[i-1]; 
       arr[0] = x; 
    } 

    /* Driver program */
    public static void main(String[] args)  
    { 
        System.out.println("Given Array is"); 
        System.out.println(Arrays.toString(arr)); 

        rotate(); 

        System.out.println("Rotated Array is"); 
        System.out.println(Arrays.toString(arr)); 
    } 
} 

```

## Python3

```py

# Python3 code for program to  
# cyclically rotate an array by one 

# Method for rotation 
def rotate(arr, n): 
    x = arr[n - 1] 

    for i in range(n - 1, 0, -1): 
        arr[i] = arr[i - 1]; 

    arr[0] = x; 

# Driver function 
arr= [1, 2, 3, 4, 5] 
n = len(arr) 
print ("Given array is") 
for i in range(0, n): 
    print (arr[i], end = ' ') 

rotate(arr, n) 

print ("\nRotated array is") 
for i in range(0, n): 
    print (arr[i], end = ' ') 

# This article is contributed  
# by saloni1297 

```

## C# 

```cs

// C# code for program to cyclically 
// rotate an array by one 
using System; 

public class Test 
{ 
    static int []arr = new int[]{1, 2, 3, 4, 5}; 

    // Method for rotation 
    static void rotate() 
    { 
    int x = arr[arr.Length - 1], i; 

    for (i = arr.Length - 1; i > 0; i--) 
        arr[i] = arr[i-1]; 
    arr[0] = x; 
    } 

    // Driver Code 
    public static void Main()  
    { 
        Console.WriteLine("Given Array is"); 
        string Original_array = string.Join(" ", arr); 
        Console.WriteLine(Original_array); 

        rotate(); 

        Console.WriteLine("Rotated Array is"); 
        string Rotated_array = string.Join(" ", arr); 
        Console.WriteLine(Rotated_array); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP code for program  
// to cyclically rotate 
// an array by one 

function rotate(&$arr, $n) 
{ 
    $x = $arr[$n - 1]; 
    for ($i = $n - 1; 
         $i > 0; $i--) 
    $arr[$i] = $arr[$i - 1];  
    $arr[0] = $x; 
} 

// Driver code 
$arr = array(1, 2, 3, 4, 5); 
$n = sizeof($arr); 

echo "Given array is \n"; 
for ($i = 0; $i < $n; $i++) 
    echo $arr[$i] . " "; 

rotate($arr, $n); 

echo "\nRotated array is\n"; 
for ($i = 0; $i < $n; $i++) 
    echo $arr[$i] . " "; 

// This code is contributed 
// by ChitraNayal 
?> 

```

**输出**：

```
Given array is
1 2 3 4 5
Rotated array is
5 1 2 3 4
```

时间复杂度：`O(n)`当我们需要遍历所有元素时。

辅助空间：`O(1)`。

通过使用[反转算法](https://www.geeksforgeeks.org/program-for-array-rotation-continued-reversal-algorithm/)也可以解决上述问题。

如果您在上述代码/算法中发现任何错误，或者找到其他解决同一问题的方法，请发表评论。

