# 数组中的最大三元组总和

> 原文： [https://www.geeksforgeeks.org/maximum-triplet-sum-array/](https://www.geeksforgeeks.org/maximum-triplet-sum-array/)

给定一个数组，任务是在数组中找到最大三元组和。

**示例**：

```
Input : arr[] = {1, 2, 3, 0, -1, 8, 10} 
Output : 21
10 + 8 + 3 = 21

Input : arr[] = {9, 8, 20, 3, 4, -1, 0}
Output : 37
20 + 9 + 8 = 37

```



**朴素的方法**：在此方法中，我们简单地运行三个循环，然后一个接一个地添加三个元素，如果三个元素的和更大，则与先前的和进行比较，然后存储在先前的和中。

## C++ 

```cpp

// C++ code to find maximum triplet sum 
#include <bits/stdc++.h> 
using namespace std; 

int maxTripletSum(int arr[], int n) 
{ 
    // Initialize sum with INT_MIN 
    int sum = INT_MIN; 

    for (int i = 0; i < n; i++) 
        for (int j = i + 1; j < n; j++) 
            for (int k = j + 1; k < n; k++)  
                if (sum < arr[i] + arr[j] + arr[k])  
                    sum = arr[i] + arr[j] + arr[k];                 
    return sum;          
} 

// Driven code 
int main() 
{ 
    int arr[] = { 1, 0, 8, 6, 4, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << maxTripletSum(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java code to find maximum triplet sum 
import java.io.*; 

class GFG { 

    static int maxTripletSum(int arr[], int n) 
    { 
        // Initialize sum with INT_MIN 
        int sum = -1000000; 

        for (int i = 0; i < n; i++) 
            for (int j = i + 1; j < n; j++) 
                for (int k = j + 1; k < n; k++)  
                    if (sum < arr[i] + arr[j] + arr[k])  
                        sum = arr[i] + arr[j] + arr[k];              
        return sum;          
    } 

    // Driven code 
    public static void main(String args[]) 
    { 
        int arr[] = { 1, 0, 8, 6, 4, 2 }; 
        int n = arr.length; 
        System.out.println(maxTripletSum(arr, n)); 
    } 
} 

// This code is contributed by Nikita Tiwari. 

```

## Python3

```py

# Python 3 code to find 
# maximum triplet sum 

def maxTripletSum(arr, n) : 

    # Initialize sum with 
    # INT_MIN 
    sm = -1000000

    for i in range(0, n) : 
        for j in range(i + 1, n) : 
            for k in range(j + 1, n) : 

                if (sm < (arr[i] + arr[j] + arr[k])) : 
                    sm = arr[i] + arr[j] + arr[k]              
    return sm 

# Driven code 
arr = [ 1, 0, 8, 6, 4, 2 ] 
n = len(arr) 

print(maxTripletSum(arr, n)) 

# This code is contributed by Nikita Tiwari. 

```

## C# 

```cs

// C# code to find maximum triplet sum 
using System; 

class GFG { 

    static int maxTripletSum(int[] arr, int n) 
    { 
        // Initialize sum with INT_MIN 
        int sum = -1000000; 

        for (int i = 0; i < n; i++) 
            for (int j = i + 1; j < n; j++) 
                for (int k = j + 1; k < n; k++) 
                    if (sum < arr[i] + arr[j] + arr[k]) 
                        sum = arr[i] + arr[j] + arr[k]; 
        return sum; 
    } 

    // Driven code 
    public static void Main() 
    { 
        int[] arr = { 1, 0, 8, 6, 4, 2 }; 
        int n = arr.Length; 
        Console.WriteLine(maxTripletSum(arr, n)); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP code to find maximum triplet sum 

function maxTripletSum( $arr, $n) 
{ 

    // Initialize sum with INT_MIN 
    $sum = PHP_INT_MIN; 

    for($i = 0; $i < $n; $i++) 
        for($j = $i + 1; $j < $n; $j++) 
            for($k = $j + 1; $k < $n; $k++)  
                if ($sum < $arr[$i] +  
                           $arr[$j] + 
                           $arr[$k]) 

                    $sum = $arr[$i] +  
                           $arr[$j] + 
                           $arr[$k];          
    return $sum;          
} 

    // Driver Code 
    $arr = array(1, 0, 8, 6, 4, 2); 
    $n = count($arr); 
    echo maxTripletSum($arr, $n); 

// This code is contributed by anuj_67\. 
?> 

```

**输出**：

```
18

```

时间复杂度：`O(n ^ 3)`。

空间复杂度：`O(1)`。

**另一种方法**：在这种情况下，我们首先需要对整个数组进行排序，然后，当我们添加数组的最后三个元素时，我们将找到三叉树的最大和。

## C++

```cpp

// C++ code to find maximum triplet sum 
#include <bits/stdc++.h> 
using namespace std; 

// This function assumes that there are at least  
// three elements in arr[]. 
int maxTripletSum(int arr[], int n) 
{ 
    // sort the given array 
    sort(arr, arr + n); 

    // After sorting the array.  
    // Add last three element of the given array 
    return arr[n - 1] + arr[n - 2] + arr[n - 3]; 
} 

// Driven code 
int main() 
{ 
    int arr[] = { 1, 0, 8, 6, 4, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << maxTripletSum(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java code to find maximum triplet sum 
import java.io.*; 
import java.util.*; 

class GFG { 

    // This function assumes that there are 
    // at least three elements in arr[]. 
    static int maxTripletSum(int arr[], int n) 
    { 
        // sort the given array 
        Arrays.sort(arr); 

        // After sorting the array.  
        // Add last three element  
        // of the given array 
        return arr[n - 1] + arr[n - 2] + arr[n - 3]; 
    }  

    // Driven code 
    public static void main(String args[]) 
    { 
        int arr[] = { 1, 0, 8, 6, 4, 2 }; 
        int n = arr.length; 
        System.out.println(maxTripletSum(arr, n)); 
    } 
} 

// This code is contributed by Nikita Tiwari. 

```

## Python3

```py

# Python 3 code to find  
# maximum triplet sum 

# This function assumes  
# that there are at least  
# three elements in arr[]. 
def maxTripletSum(arr, n) : 

    # sort the given array 
    arr.sort() 

    # After sorting the array.  
    # Add last three element  
    # of the given array 
    return (arr[n - 1] + arr[n - 2] + arr[n - 3]) 

# Driven code 
arr = [ 1, 0, 8, 6, 4, 2 ] 
n = len(arr) 

print(maxTripletSum(arr, n)) 

# This code is contributed by Nikita Tiwari. 

```

## C#

```cs

// C# code to find maximum triplet sum 
using System; 

class GFG { 

    // This function assumes that there are 
    // at least three elements in arr[]. 
    static int maxTripletSum(int[] arr, int n) 
    { 
        // sort the given array 
        Array.Sort(arr); 

        // After sorting the array. 
        // Add last three element 
        // of the given array 
        return arr[n - 1] + arr[n - 2] + arr[n - 3]; 
    } 

    // Driven code 
    public static void Main() 
    { 
        int[] arr = { 1, 0, 8, 6, 4, 2 }; 
        int n = arr.Length; 
        Console.WriteLine(maxTripletSum(arr, n)); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP code to find  
// maximum triplet sum 

// This function assumes that 
// there are at least  
// three elements in arr[]. 
function maxTripletSum( $arr, $n) 
{ 
    // sort the given array 
    sort($arr); 

    // After sorting the array.  
    // Add last three element  
    // of the given array 
    return $arr[$n - 1] + $arr[$n - 2] + 
                          $arr[$n - 3]; 
} 

// Driver code 
$arr = array( 1, 0, 8, 6, 4, 2 ); 
$n = count($arr); 
echo maxTripletSum($arr, $n); 

// This code is contributed by anuj_67\. 
?> 

```

**输出**：

```
18

```

时间复杂度：`O(nLogn)`。

空间复杂度：`O(1)`。

**有效方法**：扫描数组并计算数组中存在的最大值，第二大和第三最大元素，并返回其总和，即为最大和。

## C++

```cpp

// C++ code to find maximum triplet sum 
#include <bits/stdc++.h> 
using namespace std; 

// This function assumes that there are at least  
// three elements in arr[]. 
int maxTripletSum(int arr[], int n) 
{ 
    // Initialize Maximum, second maximum and third 
    // maximum element 
    int maxA = INT_MIN, maxB = INT_MIN, maxC = INT_MIN; 

    for (int i = 0; i < n; i++) { 

        // Update Maximum, second maximum and third 
        // maximum element 
        if (arr[i] > maxA) { 
            maxC = maxB; 
            maxB = maxA; 
            maxA = arr[i]; 
        } 

        // Update second maximum and third maximum 
        // element 
        else if (arr[i] > maxB) { 
            maxC = maxB; 
            maxB = arr[i]; 
        } 

        // Update third maximum element 
        else if (arr[i] > maxC) 
            maxC = arr[i]; 
    } 

    return (maxA + maxB + maxC); 
} 

// Driven code 
int main() 
{ 
    int arr[] = { 1, 0, 8, 6, 4, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << maxTripletSum(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java code to find maximum triplet sum 
import java.io.*; 
import java.util.*; 

class GFG { 

    // This function assumes that there  
    // are at least  three elements in arr[]. 
    static int maxTripletSum(int arr[], int n) 
    { 
        // Initialize Maximum, second maximum and third 
        // maximum element 
        int maxA = -100000000, maxB = -100000000; 
        int maxC = -100000000; 

        for (int i = 0; i < n; i++) { 

            // Update Maximum, second maximum  
            // and third maximum element 
            if (arr[i] > maxA)  
            { 
                maxC = maxB; 
                maxB = maxA; 
                maxA = arr[i]; 
            } 

            // Update second maximum and third maximum 
            // element 
            else if (arr[i] > maxB)  
            { 
                maxC = maxB; 
                maxB = arr[i]; 
            } 

            // Update third maximum element 
            else if (arr[i] > maxC) 
                maxC = arr[i]; 
        } 

        return (maxA + maxB + maxC); 
    } 

    // Driven code 
    public static void main(String args[]) 
    { 
        int arr[] = { 1, 0, 8, 6, 4, 2 }; 
        int n = arr.length; 
        System.out.println(maxTripletSum(arr, n)); 
    } 
} 

// This code is contributed by Nikita Tiwari. 

```

## Python3

```py

# Python 3 code to find  
# maximum triplet sum 

# This function assumes  
# that there are at least  
# three elements in arr[]. 
def maxTripletSum(arr, n) : 

    # Initialize Maximum, second  
    # maximum and third maximum  
    # element 
    maxA = -100000000
    maxB = -100000000
    maxC = -100000000

    for i in range(0, n) : 

        # Update Maximum, second maximum 
        # and third  maximum element 
        if (arr[i] > maxA) : 
            maxC = maxB 
            maxB = maxA 
            maxA = arr[i] 

        # Update second maximum and  
        # third maximum element 
        elif (arr[i] > maxB) : 
            maxC = maxB 
            maxB = arr[i] 

        # Update third maximum element 
        elif (arr[i] > maxC) : 
            maxC = arr[i] 

    return (maxA + maxB + maxC) 

# Driven code 
arr = [ 1, 0, 8, 6, 4, 2 ] 
n = len(arr) 

print(maxTripletSum(arr, n)) 

# This code is contributed by Nikita Tiwari. 

```

## C#

```cs

// C# code to find maximum triplet sum 
using System; 

class GFG { 

    // This function assumes that there 
    // are at least three elements in arr[]. 
    static int maxTripletSum(int[] arr, int n) 
    { 
        // Initialize Maximum, second maximum 
        // and third maximum element 
        int maxA = -100000000, maxB = -100000000; 
        int maxC = -100000000; 

        for (int i = 0; i < n; i++) { 

            // Update Maximum, second maximum 
            // and third maximum element 
            if (arr[i] > maxA) { 
                maxC = maxB; 
                maxB = maxA; 
                maxA = arr[i]; 
            } 

            // Update second maximum and third 
            // maximum element 
            else if (arr[i] > maxB) { 
                maxC = maxB; 
                maxB = arr[i]; 
            } 

            // Update third maximum element 
            else if (arr[i] > maxC) 
                maxC = arr[i]; 
        } 

        return (maxA + maxB + maxC); 
    } 

    // Driven code 
    public static void Main() 
    { 
        int[] arr = { 1, 0, 8, 6, 4, 2 }; 
        int n = arr.Length; 
        Console.WriteLine(maxTripletSum(arr, n)); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP code to find  
// maximum triplet sum 

// This function assumes that  
// there are at least three 
// elements in arr[]. 
function maxTripletSum($arr, $n) 
{ 
    // Initialize Maximum,  
    // second maximum and  
    // third maximum element 
    $maxA = PHP_INT_MIN;  
    $maxB = PHP_INT_MIN;  
    $maxC = PHP_INT_MIN; 

    for ( $i = 0; $i < $n; $i++)  
    { 

        // Update Maximum, 
        // second maximum and  
        // third maximum element 
        if ($arr[$i] > $maxA)  
        { 
            $maxC = $maxB; 
            $maxB = $maxA; 
            $maxA = $arr[$i]; 
        } 

        // Update second maximum and  
        // third maximum element 
        else if ($arr[$i] > $maxB)  
        { 
            $maxC = $maxB; 
            $maxB = $arr[$i]; 
        } 

        // Update third maximum element 
        else if ($arr[$i] > $maxC) 
            $maxC = $arr[$i]; 
    } 

    return ($maxA + $maxB + $maxC); 
} 

// Driven code 
$arr = array( 1, 0, 8, 6, 4, 2 ); 
$n = count($arr); 
echo maxTripletSum($arr, $n); 

// This code is contributed by anuj_67\. 
?> 

```

**输出**：

```
18

```

**时间复杂度**：`O(n)`。

**空间复杂度**：`O(1)`。



* * *

* * *



