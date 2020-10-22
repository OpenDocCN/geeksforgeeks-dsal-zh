# 范围总和查询（无更新）

> 原文： [https://www.geeksforgeeks.org/range-sum-queries-without-updates/](https://www.geeksforgeeks.org/range-sum-queries-without-updates/)

给定大小为`n`的整数的数组`arr`。 我们需要计算从索引`i`到索引`j`的元素总和。 由`i`和`j`索引值组成的查询将被多次执行。

例子：

```
Input : arr[] = {1, 2, 3, 4, 5}
        i = 1, j = 3
        i = 2, j = 4
Output :  9
         12         

Input : arr[] = {1, 2, 3, 4, 5}
        i = 0, j = 4 
        i = 1, j = 2 
Output : 15
          5

```



**简单解决方案**是为每个查询计算总和。

一种有效的**解决方案**是预先计算前缀和。 令`pre[i]`存储从`arr[0]`到`arr[i]`的元素之和。 为了回答查询`i, j`，我们返回`pre[j] – pre[i-1]`。

## CPP

```

// CPP program to find sum between two indexes 
// when there is no update. 
#include <bits/stdc++.h> 
using namespace std; 

void preCompute(int arr[], int n, int pre[]) 
{  
    pre[0] = arr[0]; 
    for (int i = 1; i < n; i++)  
        pre[i] = arr[i] + pre[i - 1];     
} 

// Returns sum of elements in arr[i..j] 
// It is assumed that i <= j 
int rangeSum(int i, int j, int pre[]) 
{ 
    if (i == 0) 
       return pre[j]; 

    return pre[j] - pre[i-1]; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 1, 2, 3, 4, 5 }; 
    int n = sizeof(arr)/sizeof(arr[0]); 

    int pre[n]; 
    preCompute(arr, n, pre); 
    cout << rangeSum(1, 3, pre) << endl; 
    cout << rangeSum(2, 4, pre) << endl;     

    return 0; 
} 

```

## Python3

```py

# Python program to find sum between two indexes 
# when there is no update. 

def find_ans(ar, j, k): 
    l = len(ar) 
    for i in range(1, l): 
        ar[i] = ar[i] + ar[i-1] 

    print(ar[k] - ar[j-1]) 
    return;  

pr = [1, 2, 3 ,4, 5] 
ar = pr[:] 
find_ans(ar, 1, 3) 
ar = pr[:] 
find_ans(ar, 2 ,4) 

# Code Contributed by Mohit Gupta_OMG <(0_o)> 

```

## Java

```java

// Java program to find sum between two indexes 
// when there is no update. 

import java.util.*; 
import java.lang.*; 

class GFG 
{ 
    public static void preCompute(int arr[], int n, int pre[]) 
    { 
        pre[0] = arr[0]; 
        for (int i = 1; i < n; i++) 
            pre[i] = arr[i] + pre[i - 1]; 
    } 

    // Returns sum of elements in arr[i..j] 
    // It is assumed that i <= j 
    public static int rangeSum(int i, int j, int pre[]) 
    { 
        if (i == 0) 
            return pre[j]; 

        return pre[j] - pre[i-1]; 
    } 

    public static void main(String[] args) 
    { 
        int arr[] = { 1, 2, 3, 4, 5 }; 
        int n = arr.length; 

        int pre[] = new int[n]; 

        preCompute(arr, n, pre); 
        System.out.println(rangeSum(1, 3, pre)); 
        System.out.println(rangeSum(2, 4, pre)); 

    } 
} 

// Code Contributed by Mohit Gupta_OMG <(0_o)> 

```

## C# 

```cs

// Program to find sum between two 
// indexes when there is no update. 
using System; 

class GFG { 
    public static void preCompute(int[] arr, int n, int[] pre) 
    { 
        pre[0] = arr[0]; 
        for (int i = 1; i < n; i++) 
            pre[i] = arr[i] + pre[i - 1]; 
    } 

    // Returns sum of elements in 
    // arr[i..j] 
    // It is assumed that i <= j 
    public static int rangeSum(int i, int j, int[] pre) 
    { 
        if (i == 0) 
            return pre[j]; 

        return pre[j] - pre[i - 1]; 
    } 

    // Driver code 
    public static void Main() 
    { 
        int[] arr = { 1, 2, 3, 4, 5 }; 
        int n = arr.Length; 

        int[] pre = new int[n]; 

        preCompute(arr, n, pre); 
        Console.WriteLine(rangeSum(1, 3, pre)); 
        Console.WriteLine(rangeSum(2, 4, pre)); 
    } 
} 

// Code Contributed by Anant Agarwal. 

```

**输出**：

```
9
12

```

在这里，每个范围总和查询的时间复杂度为`O(1)`。

当还允许更新时，问题变得复杂。 在这种情况下，请使用高级数据结构，例如[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)或[二叉索引树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)。


