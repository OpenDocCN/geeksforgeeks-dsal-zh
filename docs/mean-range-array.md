# 数组范围的平均值

> 原文： [https://www.geeksforgeeks.org/mean-range-array/](https://www.geeksforgeeks.org/mean-range-array/)

给定`n`个整数数组。 给出`q`个查询。 编写一个程序，在新行中为每个查询打印从`l`到`r`范围内的均值的下限值。

**示例**：

```
Input : arr[] = {1, 2, 3, 4, 5}
        q = 3
        0 2
        1 3
        0 4
Output : 2
         3
         3
Here for 0 to 2 (1 + 2 + 3) / 3 = 2

Input : arr[] = {6, 7, 8, 10}
        q = 2
        0 3
        1 2
Output : 7
         7

```



**朴素的方法**：我们可以为每个查询`l`到`r`运行循环，并找到范围内元素的总和和数量。 此后，我们可以为每个查询打印均值下限。

## C++ 

```cpp

// CPP program to find floor value 
// of mean in range l to r 
#include <bits/stdc++.h> 
using namespace std; 

// To find mean of range in l to r 
int findMean(int arr[], int l, int r) 
{ 
    // Both sum and count are 
    // initialize to 0 
    int sum = 0, count = 0; 

    // To calculate sum and number 
    // of elements in range l to r 
    for (int i = l; i <= r; i++) { 
        sum += arr[i]; 
        count++; 
    } 

    // Calculate floor value of mean 
    int mean = floor(sum / count); 

    // Returns mean of array 
    // in range l to r 
    return mean; 
} 

// Driver program to test findMean() 
int main() 
{ 
    int arr[] = { 1, 2, 3, 4, 5 }; 
    cout << findMean(arr, 0, 2) << endl; 
    cout << findMean(arr, 1, 3) << endl; 
    cout << findMean(arr, 0, 4) << endl; 
    return 0; 
} 

```