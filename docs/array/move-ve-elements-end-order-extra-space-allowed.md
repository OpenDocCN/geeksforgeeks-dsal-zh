# 将所有负元素移动到最后，并留出足够的空间

> 原文： [https://www.geeksforgeeks.org/move-ve-elements-end-order-extra-space-allowed/](https://www.geeksforgeeks.org/move-ve-elements-end-order-extra-space-allowed/)

给定一个未排序的正负整数数组。 任务是将所有负元素放置在数组的末尾，而不更改正元素和负元素的顺序。

**示例**：

```
Input : arr[] = {1, -1, 3, 2, -7, -5, 11, 6 }
Output : 1  3  2  11  6  -1  -7  -5 

Input : arr[] = {-5, 7, -3, -4, 9, 10, -1, 11}
Output : 7  9  10  11  -5  -3  -4  -1  

```



我们在下面的文章中讨论了解决此问题的不同方法。

[使用恒定的额外空间重新排列正数和负数](https://www.geeksforgeeks.org/rearrange-positive-and-negative-numbers/)

如果允许我们使用额外的空间，问题将变得更加容易。 想法是创建一个空数组（`temp[]`）。 首先，我们存储给定数组的所有正元素，然后将数组的所有负元素存储在`Temp[]`中。 最后，我们将`temp[]`复制到原始数组。

以下是上述想法的实现：

## C/C++ 

```

// C++ program to Move All -ve Element At End 
// Without changing order Of Array Element 
#include<bits/stdc++.h> 
using namespace std; 

// Moves all -ve element to end of array in 
// same order. 
void segregateElements(int arr[], int n) 
{ 
    // Create an empty array to store result 
    int temp[n]; 

    // Traversal array and store +ve element in 
    // temp array 
    int j = 0; // index of temp 
    for (int i = 0; i < n ; i++) 
        if (arr[i] >= 0 ) 
            temp[j++] = arr[i]; 

    // If array contains all positive or all negative. 
    if (j == n || j == 0) 
        return; 

    // Store -ve element in temp array 
    for (int i = 0 ; i < n ; i++) 
        if (arr[i] < 0) 
            temp[j++] = arr[i]; 

    // Copy contents of temp[] to arr[] 
    memcpy(arr, temp, sizeof(temp)); 
} 

// Driver program 
int main() 
{ 
    int arr[] = {1 ,-1 ,-3 , -2, 7, 5, 11, 6 }; 
    int n = sizeof(arr)/sizeof(arr[0]); 

    segregateElements(arr, n); 

    for (int i = 0; i < n; i++) 
       cout << arr[i] << " "; 

    return 0; 
} 

```

## Java

```java
// Java program to Move All -ve Element At End 
// Without changing order Of Array Element 
import java.util.Arrays; 
  
class GFG { 
      
    // Moves all -ve element to end of array in 
    // same order. 
    static void segregateElements(int arr[], int n) 
    { 
          
        // Create an empty array to store result 
        int temp[] = new int[n]; 
  
        // Traversal array and store +ve element in 
        // temp array 
        int j = 0; // index of temp 
          
        for (int i = 0; i < n; i++) 
            if (arr[i] >= 0) 
                temp[j++] = arr[i]; 
  
        // If array contains all positive or all  
        // negative. 
        if (j == n || j == 0) 
            return; 
  
        // Store -ve element in temp array 
        for (int i = 0; i < n; i++) 
            if (arr[i] < 0) 
                temp[j++] = arr[i]; 
  
        // Copy contents of temp[] to arr[] 
        for (int i = 0; i < n; i++) 
            arr[i] = temp[i]; 
    } 
      
    // Driver code 
    public static void main(String arg[]) 
    { 
        int arr[] = { 1, -1, -3, -2, 7, 5, 11, 6 }; 
        int n = arr.length; 
  
        segregateElements(arr, n); 
  
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i] + " "); 
    } 
} 
  
// This code is contributed by Anant Agarwal. 
```

## Python

```py
# Python program to Move All -ve Element At End 
# Without changing order Of Array Element 
   
# Moves all -ve element to end of array in 
# same order. 
def segregateElements(arr, n): 
    # Create an empty array to store result 
    temp = [0 for k in range(n)] 
   
    # Traversal array and store +ve element in 
    # temp array 
    j = 0 # index of temp 
    for i in range(n): 
        if (arr[i] >= 0 ): 
            temp[j] = arr[i] 
            j +=1
   
    # If array contains all positive or all negative. 
    if (j == n or j == 0): 
        return
   
    # Store -ve element in temp array 
    for i in range(n): 
        if (arr[i] < 0): 
            temp[j] = arr[i] 
            j +=1
   
    # Copy contents of temp[] to arr[] 
    for k in range(n): 
        arr[k] = temp[k] 
  
# Driver program 
arr = [1 ,-1 ,-3 , -2, 7, 5, 11, 6 ] 
n = len(arr) 
  
segregateElements(arr, n); 
   
for i in range(n): 
    print arr[i], 
  
# Contributed by Afzal aka Saan 
```

## C#

```cs
// C# program to Move All -ve Element At End 
// Without changing order Of Array Element 
using System; 
  
class GFG { 
  
    // Moves all -ve element to  
    // end of array in same order. 
    static void segregateElements(int[] arr, int n) 
    { 
        // Create an empty array to store result 
        int[] temp = new int[n]; 
  
        // Traversal array and store +ve element in 
        // temp array 
        int j = 0; // index of temp 
  
        for (int i = 0; i < n; i++) 
            if (arr[i] >= 0) 
                temp[j++] = arr[i]; 
  
        // If array contains all positive or all 
        // negative. 
        if (j == n || j == 0) 
            return; 
  
        // Store -ve element in temp array 
        for (int i = 0; i < n; i++) 
            if (arr[i] < 0) 
                temp[j++] = arr[i]; 
  
        // Copy contents of temp[] to arr[] 
        for (int i = 0; i < n; i++) 
            arr[i] = temp[i]; 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int[] arr = { 1, -1, -3, -2, 7, 5, 11, 6 }; 
        int n = arr.Length; 
        segregateElements(arr, n); 
  
        for (int i = 0; i < n; i++) 
            Console.Write(arr[i] + " "); 
    } 
} 
  
// This Code is contributed by vt_m. 
```

## PHP

```php
<?php  
// PHP program to Move All -ve Element At End 
// Without changing order Of Array Element 
  
// Moves all -ve element to end of  
// array in same order. 
function segregateElements(&$arr, $n) 
{ 
    // Create an empty array to store result 
    $temp = array(0, $n, NULL); 
  
    // Traversal array and store +ve  
    // element in temp array 
    $j = 0; // index of temp 
    for ($i = 0; $i < $n ; $i++) 
        if ($arr[$i] >= 0 ) 
            $temp[$j++] = $arr[$i]; 
  
    // If array contains all positive  
    // or all negative. 
    if ($j == $n || $j == 0) 
        return; 
  
    // Store -ve element in temp array 
    for ($i = 0 ; $i < $n ; $i++) 
        if ($arr[$i] < 0) 
            $temp[$j++] = $arr[$i]; 
  
    // Copy contents of temp[] to arr[] 
    for($i = 0; $i < $n; $i++) 
        $arr[$i] = $temp[$i]; 
} 
  
// Driver Code 
$arr = array(1 ,-1 ,-3 , -2, 7, 5, 11, 6 ); 
$n = sizeof($arr); 
  
segregateElements($arr, $n); 
  
for ($i = 0; $i < $n; $i++) 
echo $arr[$i] ." "; 
  
// This code is contributed  
// by ChitraNayal 
?> 
```

输出：

```
1 7 5 11 6 -1 -3 -2 
```

时间复杂度：`O(n)`。

辅助空间：`O(n)`。
