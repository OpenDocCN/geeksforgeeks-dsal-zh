# 在给定的数组中找到一个固定点（等于索引的值）

> 原文： [https://www.geeksforgeeks.org/find-a-fixed-point-in-a-given-array/](https://www.geeksforgeeks.org/find-a-fixed-point-in-a-given-array/)

给定一个由`n`个不同的整数组成的数组，这些数组按升序排序，如果数组中存在固定点，则编写一个返回固定点的函数，否则返回 -1。 数组中的不动点是索引`i`，因此`arr[i]`等于`i`。 请注意，数组中的整数可以为负数。

例子：

```
  Input: arr[] = {-10, -5, 0, 3, 7}
  Output: 3  // arr[3] == 3 

  Input: arr[] = {0, 2, 5, 8, 17}
  Output: 0  // arr[0] == 0 

  Input: arr[] = {-10, -5, 3, 4, 7, 9}
  Output: -1  // No Fixed Point

```



**方法 1（线性搜索）**：

线性搜索索引`i`，以使`arr[i] == i`。 返回找到的第一个这样的索引。 感谢 pm 建议这种解决方案。

## C++ 

```cpp

// C++ program to check fixed point  
// in an array using linear search  
#include <bits/stdc++.h> 
using namespace std; 

int linearSearch(int arr[], int n)  
{  
    int i;  
    for(i = 0; i < n; i++)  
    {  
        if(arr[i] == i)  
            return i;  
    }  

    /* If no fixed point present then return -1 */
    return -1;  
}  

/* Driver code */
int main()  
{  
    int arr[] = {-10, -1, 0, 3, 10, 11, 30, 50, 100};  
    int n = sizeof(arr)/sizeof(arr[0]);  
    cout << "Fixed Point is " << linearSearch(arr, n);  
    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## C

```
// C program to check fixed point  
// in an array using linear search 
#include<stdio.h> 
  
int linearSearch(int arr[], int n) 
{ 
    int i; 
    for(i = 0; i < n; i++) 
    { 
        if(arr[i] == i) 
            return i; 
    } 
  
    /* If no fixed point present then return -1 */
    return -1; 
} 
  
/* Driver program to check above functions */
int main() 
{ 
    int arr[] = {-10, -1, 0, 3, 10, 11, 30, 50, 100}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    printf("Fixed Point is %d", linearSearch(arr, n)); 
    getchar(); 
    return 0; 
}
```

## Java

```
// Java program to check fixed point  
// in an array using linear search 
   
class Main 
{ 
    static int linearSearch(int arr[], int n) 
    { 
        int i; 
        for(i = 0; i < n; i++) 
        { 
            if(arr[i] == i) 
                return i; 
        } 
        
        /* If no fixed point present  
           then return -1 */
        return -1; 
    } 
    //main function 
    public static void main(String args[]) 
    { 
        int arr[] = {-10, -1, 0, 3, 10, 11, 30, 50, 100}; 
        int n = arr.length; 
        System.out.println("Fixed Point is " 
                     + linearSearch(arr, n)); 
    } 
}
```

## Python

```
# Python program to check fixed point  
# in an array using linear search 
def linearSearch(arr, n): 
    for i in range(n): 
        if arr[i] is i: 
            return i 
    # If no fixed point present then return -1 
    return -1
  
# Driver program to check above functions 
arr = [-10, -1, 0, 3, 10, 11, 30, 50, 100] 
n = len(arr) 
print("Fixed Point is " + str(linearSearch(arr,n))) 
  
# This code is contributed by Pratik Chhajer
```

## C#

```
// C# program to check fixed point  
// in an array using linear search 
using System; 
  
class GFG 
{ 
    static int linearSearch(int []arr, int n) 
    { 
        int i; 
        for(i = 0; i < n; i++) 
        { 
            if(arr[i] == i) 
                return i; 
        } 
          
        /* If no fixed point present  
        then return -1 */
        return -1; 
    } 
    // Driver code 
    public static void Main() 
    { 
        int []arr = {-10, -1, 0, 3, 10, 11, 30, 50, 100}; 
        int n = arr.Length; 
        Console.Write("Fixed Point is "+ linearSearch(arr, n)); 
    } 
} 
  
// This code is contributed by Sam007
```

## PHP

```
<?php 
// PHP program to check fixed point  
// in an array using linear search 
  
function linearSearch($arr, $n) 
{ 
    for($i = 0; $i < $n; $i++) 
    { 
        if($arr[$i] == $i) 
            return $i; 
    } 
  
    // If no fixed point present then 
    // return -1 
    return -1; 
} 
  
    // Driver Code 
    $arr = array(-10, -1, 0, 3, 10,  
                  11, 30, 50, 100); 
    $n = count($arr); 
    echo "Fixed Point is ". 
            linearSearch($arr,$n); 
  
// This code is contributed by Sam007 
?>
```

输出：

```
Fixed Point is 3
```

时间复杂度：`O(n)`。