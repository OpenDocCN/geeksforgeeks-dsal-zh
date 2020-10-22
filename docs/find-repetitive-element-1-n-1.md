# 查找 1 到`n-1`之间的唯一重复元素

> 原文： [https://www.geeksforgeeks.org/find-repetitive-element-1-n-1/](https://www.geeksforgeeks.org/find-repetitive-element-1-n-1/)

给我们一个大小为`n`的数组`arr[]`。 数字从 1 到`n-1`以随机顺序排列。 该数组只有一个重复元素。 我们需要找到重复元素。

**示例**：

```
Input  : a[] = {1, 3, 2, 3, 4}
Output : 3

Input  : a[] = {1, 5, 1, 2, 3, 4}
Output : 1

```



**方法 1（简单）**我们使用两个嵌套循环。 外循环遍历所有元素，内循环检查外循环拾取的元素是否出现在其他任何地方。

**时间复杂度**：`O(n * n)`。

**方法 2（使用求和公式）**：我们知道[前`n-1`个自然数](https://www.geeksforgeeks.org/program-find-sum-first-n-natural-numbers/)的和为`(n – 1) * n / 2`。 我们计算数组元素的总和，并从中减去自然数总和，以找到唯一的缺失元素。

## C++ 

```cpp

// CPP program to find the only repeating 
// element in an array where elements are 
// from 1 to n-1\. 
#include <bits/stdc++.h> 
using namespace std; 

int findRepeating(int arr[], int n) 
{ 
   // Find array sum and subtract sum 
   // first n-1 natural numbers from it 
   // to find the result. 
   return accumulate(arr , arr+n , 0) -  
                   ((n - 1) * n/2); 
} 

// driver code 
int main() 
{    
    int arr[] = { 9, 8, 2, 6, 1, 8, 5, 3, 4, 7 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << findRepeating(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find the only repeating  
// element in an array where elements are  
// from 1 to n-1\. 
import java.io.*; 
import java.util.*;  

class GFG  
{ 

    static int findRepeating(int[] arr, int n) 
    { 
        // Find array sum and subtract sum  
        // first n-1 natural numbers from it  
        // to find the result. 

        int sum = 0; 
        for (int i = 0; i < n; i++) 
            sum += arr[i]; 
        return sum - (((n - 1) * n) / 2);  
    } 

    // Driver code 
    public static void main(String args[])  
    { 
        int[] arr = { 9, 8, 2, 6, 1, 8, 5, 3, 4, 7 }; 
        int n = arr.length; 
        System.out.println(findRepeating(arr, n)); 
    } 
} 

// This code is contributed by rachana soma 

```

## Python3

```py

# Python3 program to find the only  
# repeating element in an array where  
# elements are from 1 to n-1\. 

def findRepeating(arr, n): 

    # Find array sum and subtract sum 
    # first n-1 natural numbers from it 
    # to find the result. 
    return sum(arr) -(((n - 1) * n) // 2) 

# Driver Code 
arr = [9, 8, 2, 6, 1, 8, 5, 3, 4, 7] 
n = len(arr) 
print(findRepeating(arr, n)) 

# This code is contributed  
# by mohit kumar 

```

## C# 

```cs

// C# program to find the only repeating  
// element in an array where elements are  
// from 1 to n-1\. 
using System;  

class GFG  
{ 

    static int findRepeating(int[] arr, int n) 
    { 
        // Find array sum and subtract sum  
        // first n-1 natural numbers from it  
        // to find the result. 

        int sum = 0; 
        for (int i = 0; i < n; i++) 
            sum += arr[i]; 
        return sum - (((n - 1) * n) / 2);  
    } 

    // Driver code 
    public static void Main(String []args)  
    { 
        int[] arr = { 9, 8, 2, 6, 1, 8, 5, 3, 4, 7 }; 
        int n = arr.Length; 
        Console.WriteLine(findRepeating(arr, n)); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**输出**：

```
8

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(1)`。

导致大型数组溢出。

**方法 3（使用散列）**：使用散列表存储已访问的元素。 如果看到的元素再次出现，我们将其返回。

## C++

```cpp

// CPP program to find the only repeating 
// element in an array where elements are 
// from 1 to n-1\. 
#include <bits/stdc++.h> 
using namespace std; 

int findRepeating(int arr[], int n) 
{ 
   unordered_set<int> s; 
   for (int i=0; i<n; i++) 
   { 
      if (s.find(arr[i]) != s.end()) 
         return arr[i]; 
      s.insert(arr[i]); 
   } 

   // If input is correct, we should  
   // never reach here 
   return -1; 
} 

// driver code 
int main() 
{    
    int arr[] = { 9, 8, 2, 6, 1, 8, 5, 3, 4, 7 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << findRepeating(arr, n); 
    return 0; 
} 

```

## Java

```java

import java.util.*; 
// Java program to find the only repeating  
// element in an array where elements are  
// from 1 to n-1\. 

class GFG  
{ 

static int findRepeating(int arr[], int n)  
{  
    HashSet<Integer> s = new HashSet<Integer>(); 
    for (int i = 0; i < n; i++)  
    {  
        if (s.contains(arr[i]))  
            return arr[i];  
        s.add(arr[i]);  
    }  

    // If input is correct, we should  
    // never reach here  
    return -1;  
}  

// Driver code  
public static void main(String[] args)  
{ 
    int arr[] = { 9, 8, 2, 6, 1, 8, 5, 3, 4, 7 };  
    int n = arr.length; 
    System.out.println(findRepeating(arr, n));; 
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python3

```py

# Python3 program to find the only  
# repeating element in an array  
# where elements are from 1 to n-1.  
def findRepeating(arr, n): 
    s = set() 
    for i in range(n): 
        if arr[i] in s: 
            return arr[i] 
        s.add(arr[i]) 

    # If input is correct, we should  
    # never reach here  
    rteurn -1

# Driver code 
arr = [9, 8, 2, 6, 1, 8, 5, 3] 
n = len(arr) 
print(findRepeating(arr, n)) 

# This code is contributed  
# by Shrikant13 

```

## C#

```cs

// C# program to find the only repeating  
// element in an array where elements are  
// from 1 to n-1\. 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

static int findRepeating(int []arr, int n)  
{  
    HashSet<int> s = new HashSet<int>(); 
    for (int i = 0; i < n; i++)  
    {  
        if (s.Contains(arr[i]))  
            return arr[i];  
        s.Add(arr[i]);  
    }  

    // If input is correct, we should  
    // never reach here  
    return -1;  
}  

// Driver code  
public static void Main(String[] args)  
{ 
    int []arr = { 9, 8, 2, 6, 1, 8, 5, 3, 4, 7 };  
    int n = arr.Length; 
    Console.WriteLine(findRepeating(arr, n));; 
} 
} 

// This code has been contributed by 29AjayKumar 

```

**输出**：

```
8

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(n)`。

**方法 4（使用 XOR）**：该思想基于以下事实：`x ^ x = 0`且`x ^ y = y ^ x`。

1.  计算从 1 到`n-1`的元素的 XOR。

2.  计算数组元素的 XOR。

3.  以上两项的异或将是我们的结果。

## C++

```cpp

// CPP program to find the only repeating 
// element in an array where elements are 
// from 1 to n-1\. 
#include <bits/stdc++.h> 
using namespace std; 

int findRepeating(int arr[], int n) 
{ 

   // res is going to store value of 
   // 1 ^ 2 ^ 3 .. ^ (n-1) ^ arr[0] ^  
   // arr[1] ^ .... arr[n-1] 
   int res = 0; 
   for (int i=0; i<n-1; i++) 
       res = res ^ (i+1) ^ arr[i]; 
   res = res ^ arr[n-1]; 

   return res; 
} 

// driver code 
int main() 
{    
    int arr[] = { 9, 8, 2, 6, 1, 8, 5, 3, 4, 7 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << findRepeating(arr, n); 
    return 0; 
} 

```

## Java

```java
// Java program to find the only repeating 
// element in an array where elements are 
// from 1 to n-1. 
class GFG 
{ 
      
    static int findRepeating(int arr[], int n) 
    { 
      
        // res is going to store value of 
        // 1 ^ 2 ^ 3 .. ^ (n-1) ^ arr[0] ^  
        // arr[1] ^ .... arr[n-1] 
        int res = 0; 
        for (int i = 0; i < n - 1; i++) 
            res = res ^ (i + 1) ^ arr[i]; 
        res = res ^ arr[n - 1]; 
              
        return res; 
    } 
      
    // Driver code 
    public static void main(String[] args) 
    {  
        int arr[] = { 9, 8, 2, 6, 1, 8, 5, 3, 4, 7 }; 
        int n = arr.length; 
        System.out.println(findRepeating(arr, n)); 
    } 
} 
  
// This code is contributed by  
// Smitha Dinesh Semwal.
```

## Python3

```py
# Python3 program to find the only  
# repeating element in an array where  
# elements are from 1 to n-1. 
  
def findRepeating(arr, n): 
      
    # res is going to store value of 
    # 1 ^ 2 ^ 3 .. ^ (n-1) ^ arr[0] ^  
    # arr[1] ^ .... arr[n-1] 
    res = 0
    for i in range(0, n-1): 
        res = res ^ (i+1) ^ arr[i] 
    res = res ^ arr[n-1] 
          
    return res 
      
# Driver code 
arr = [9, 8, 2, 6, 1, 8, 5, 3, 4, 7]  
n = len(arr)  
print(findRepeating(arr, n)) 
  
# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```cs
// C# program to find the  
// only repeating element  
// in an array where elements  
// are from 1 to n-1. 
using System; 
  
class GFG 
{ 
    static int findRepeating(int []arr,  
                             int n) 
    { 
      
        // res is going to store  
        // value of 1 ^ 2 ^ 3 ..  
        // ^ (n-1) ^ arr[0] ^  
        // arr[1] ^ .... arr[n-1] 
        int res = 0; 
        for (int i = 0; i < n - 1; i++) 
            res = res ^ (i + 1) ^ arr[i]; 
        res = res ^ arr[n - 1]; 
              
        return res; 
    } 
      
    // Driver code 
    public static void Main() 
    {  
        int []arr = { 9, 8, 2, 6, 1,  
                      8, 5, 3, 4, 7 }; 
        int n = arr.Length; 
        Console.Write(findRepeating(arr, n)); 
    } 
} 
  
// This code is contributed 
// by Smitha Dinesh Semwal.
```

## PHP

```php
<?php 
// PHP program to find the only repeating 
// element in an array where elements are 
// from 1 to n-1. 
  
function findRepeating($arr, $n) 
{ 
  
    // res is going to store value of 
    // 1 ^ 2 ^ 3 .. ^ (n-1) ^ arr[0] ^  
    // arr[1] ^ .... arr[n-1] 
    $res = 0; 
    for($i = 0; $i < $n - 1; $i++) 
        $res = $res ^ ($i + 1) ^ $arr[$i]; 
    $res = $res ^ $arr[$n - 1]; 
          
    return $res; 
} 
  
    // Driver Code 
    $arr =array(9, 8, 2, 6, 1, 8, 5, 3, 4, 7); 
    $n = sizeof($arr) ; 
    echo findRepeating($arr, $n); 
      
// This code is contributed by ajit 
?>
```

输出：

```
8
```

时间复杂度：`O(n)`。

辅助空间：`O(1)`。

方法 5：使用索引。

1.  遍历数组。
2.  对于每个索引访问`a[index]`，如果为正，则更改`a[index]`索引处元素的符号，否则打印该元素。

## C++

```cpp
// CPP program to find the only  
// repeating element in an array  
// where elements are from 1 to n-1. 
#include <bits/stdc++.h> 
using namespace std; 
  
// Function to find repeted element 
int findRepeating(int arr[], int n) 
{ 
    int missingElement = 0; 
  
    // indexing based 
    for (int i = 0; i < n; i++){ 
  
        int element = arr[abs(arr[i])]; 
  
        if(element < 0){ 
            missingElement = arr[i]; 
            break; 
        } 
      
    arr[abs(arr[i])] = -arr[abs(arr[i])]; 
} 
  
return abs(missingElement); 
  
} 
  
// driver code 
int main() 
{ 
    int arr[] = { 5, 4, 3, 9, 8, 
                  9, 1, 6, 2, 5}; 
  
    int n = sizeof(arr) / sizeof(arr[0]); 
  
    cout << findRepeating(arr, n); 
  
    return 0; 
}
```

## Java

```java
// Java program to find the only  
// repeating element in an array  
// where elements are from 1 to n-1. 
import java.lang.Math.*; 
  
class GFG 
{ 
    // Function to find repeted element 
    static int findRepeating(int arr[], int n) 
    { 
        int missingElement = 0; 
      
        // indexing based 
        for (int i = 0; i < n; i++){ 
      
            int element = arr[Math.abs(arr[i])]; 
      
            if(element < 0){ 
                missingElement = arr[i]; 
                break; 
            } 
          
        arr[Math.abs(arr[i])] = -arr[Math.abs(arr[i])]; 
    } 
      
    return Math.abs(missingElement); 
      
    } 
      
    // Driver code 
    public static void main(String[] args) 
    { 
        int arr[] = { 5, 4, 3, 9, 8, 
                    9, 1, 6, 2, 5}; 
      
        int n = arr.length; 
      
        System.out.println(findRepeating(arr, n)); 
      
    } 
} 
// This code is contributed by  
// Smitha Dinesh Semwal.
```

## Python3

```py
# Python3 program to find the only  
# repeating element in an array  
# where elements are from 1 to n-1. 
  
# Function to find repeted element 
def findRepeating(arr, n): 
  
    missingElement = 0
  
    # indexing based 
    for i in range(0, n): 
  
        element = arr[abs(arr[i])] 
  
        if(element < 0): 
            missingElement = arr[i] 
            break
          
        arr[abs(arr[i])] = -arr[abs(arr[i])] 
      
    return abs(missingElement) 
  
# Driver code 
arr = [5, 4, 3, 9, 8, 9, 1, 6, 2, 5] 
n = len(arr) 
print(findRepeating(arr, n)) 
  
# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```cs
using System; 
  
// C# program to find the only  
// repeating element in an array  
// where elements are from 1 to n-1.  
  
  
public class GFG 
{ 
    // Function to find repeted element  
    public static int findRepeating(int[] arr, int n) 
    { 
        int missingElement = 0; 
  
        // indexing based  
        for (int i = 0; i < n; i++) 
        { 
  
            int element = arr[Math.Abs(arr[i])]; 
  
            if (element < 0) 
            { 
                missingElement = arr[i]; 
                break; 
            } 
  
        arr[Math.Abs(arr[i])] = -arr[Math.Abs(arr[i])]; 
        } 
  
    return Math.Abs(missingElement); 
  
    } 
  
    // Driver code  
    public static void Main(string[] args) 
    { 
        int[] arr = new int[] {5, 4, 3, 9, 8, 9, 
                                1, 6, 2, 5}; 
  
        int n = arr.Length; 
  
        Console.WriteLine(findRepeating(arr, n)); 
  
    } 
} 
  
// This code is contributed by Shrikant13
```

## PHP

```php
<?php 
// PHP program to find the only  
// repeating element in an array  
// where elements are from 1 to n-1. 
  
// Function to find repeted element 
function findRepeating($arr, $n) 
{ 
    $missingElement = 0; 
  
    // indexing based 
    for ($i = 0; $i < $n; $i++) 
    { 
  
        $element = $arr[abs($arr[$i])]; 
  
        if($element < 0) 
        { 
            $missingElement = $arr[$i]; 
            break; 
        } 
      
    $arr[abs($arr[$i])] = -$arr[abs($arr[$i])]; 
} 
  
return abs($missingElement); 
  
} 
  
// Driver Code 
$arr = array (5, 4, 3, 9, 8, 
              9, 1, 6, 2, 5); 
  
$n = sizeof($arr); 
  
echo findRepeating($arr, $n); 
  
// This code is contributed by ajit 
?>
```

输出：

```
9
```

时间复杂度：`O(n)`。

辅助空间：`O(1)`。