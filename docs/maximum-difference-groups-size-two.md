# 大小为 2 的分组之间的最大差异

> 原文： [https://www.geeksforgeeks.org/maximum-difference-groups-size-two/](https://www.geeksforgeeks.org/maximum-difference-groups-size-two/)

给定一个偶数个元素的数组，请使用这些数组元素形成 2 个组，以使总和最高的组与总和最低的组之间的差最大。

**注意**：一个元素只能是一个组的一部分，并且必须是至少一个组的一部分。

**示例**：

```
Input : arr[] = {1, 4, 9, 6}
Output : 10
Groups formed will be (1, 4) and (6, 9), 
the difference between highest sum group
(6, 9) i.e 15 and lowest sum group (1, 4)
i.e 5 is 10.

Input : arr[] = {6, 7, 1, 11}
Output : 11
Groups formed will be (1, 6) and (7, 11), 
the difference between highest sum group
(7, 11) i.e 18 and lowest sum group (1, 6)
i.e 7 is 11.

```



**简单方法**：我们可以通过进行所有可能的组合并检查最高和最低组之间的每组组合差异来解决此问题。 总共将形成`n * (n-1) / 2`个这样的基团`C(n, 2)`。

时间复杂度：`O(n ^ 3)`，因为将花费`O(n ^ 2)`来生成组并检查每个组`n`次迭代，因此总体上需要`O(n ^ 3)`时间。

**有效方法**：我们可以使用贪婪方法。 对整个数组进行排序，我们的结果是最后两个元素的总和减去前两个元素的总和。

## C++ 

```cpp

// CPP program to find minimum difference 
// between groups of highest and lowest 
// sums. 
#include <bits/stdc++.h> 
#define ll long long int 
using namespace std; 

ll CalculateMax(ll arr[], int n) 
{ 
    // Sorting the whole array. 
    sort(arr, arr + n); 

    int min_sum = arr[0] + arr[1]; 
    int max_sum = arr[n-1] + arr[n-2]; 

    return abs(max_sum - min_sum); 
} 

// Driver code 
int main() 
{ 
    ll arr[] = { 6, 7, 1, 11 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << CalculateMax(arr, n) << endl; 
    return 0; 
} 

```

## Java

```java

// Java program to find minimum difference  
// between groups of highest and lowest  
// sums.  
import java.util.Arrays;  
import java.io.*; 

class GFG { 
static int  CalculateMax(int  arr[], int n)  
{  
    // Sorting the whole array.  
    Arrays.sort(arr);  

    int min_sum = arr[0] + arr[1];  
    int max_sum = arr[n-1] + arr[n-2];  

    return (Math.abs(max_sum - min_sum));  
}  

// Driver code 

    public static void main (String[] args) { 

    int arr[] = { 6, 7, 1, 11 };  
    int n = arr.length;  
    System.out.println (CalculateMax(arr, n));  
    } 
} 

```

## Python3

```py

# Python 3 program to find minimum difference  
# between groups of highest and lowest  
def CalculateMax(arr, n): 

    # Sorting the whole array. 
    arr.sort() 
    min_sum = arr[0] + arr[1] 
    max_sum = arr[n - 1] + arr[n - 2] 
    return abs(max_sum - min_sum) 

# Driver code 
arr = [6, 7, 1, 11] 
n = len(arr) 
print(CalculateMax(arr, n)) 

# This code is contributed 
# by Shrikant13 

```

## C# 

```cs

// C# program to find minimum difference  
// between groups of highest and lowest  
// sums. 
using System; 

public class GFG{ 

static int CalculateMax(int []arr, int n)  
{  
    // Sorting the whole array.  
    Array.Sort(arr);  

    int min_sum = arr[0] + arr[1];  
    int max_sum = arr[n-1] + arr[n-2];  

    return (Math.Abs(max_sum - min_sum));  
}  

// Driver code 

    static public void Main (){ 
    int []arr = { 6, 7, 1, 11 };  
    int n = arr.Length;  
    Console.WriteLine(CalculateMax(arr, n));  
    } 
//This code is contributed by Sachin.     
} 

```

## PHP

```php

<?php 
// PHP program to find minimum  
// difference between groups of  
// highest and lowest sums. 
function CalculateMax($arr, $n) 
{ 
    // Sorting the whole array. 
    sort($arr); 

    $min_sum = $arr[0] +  
               $arr[1]; 
    $max_sum = $arr[$n - 1] +  
               $arr[$n - 2]; 

    return abs($max_sum - 
               $min_sum); 
} 

// Driver code 
$arr = array (6, 7, 1, 11 ); 
$n = sizeof($arr); 
echo CalculateMax($arr, $n), "\n" ; 

// This code is contributed by ajit 
?> 

```

**输出**：

```
11

```

**时间复杂度**：`O(n * log n)`。

**进一步优化**：

除了排序，我们还可以在线性时间中找到最大 2 个和最小 2 个，并将时间复杂度降低到`O(n)`。

[](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *



