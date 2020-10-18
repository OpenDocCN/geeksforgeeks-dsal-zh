# 数组元素的频率范围查询

> 原文： [https://www.geeksforgeeks.org/range-queries-for-frequencies-of-array-elements/](https://www.geeksforgeeks.org/range-queries-for-frequencies-of-array-elements/)

给定`n`个非负整数的数组。 任务是在`array[]`的任意范围内查找特定元素的频率。 范围以数组中的位置（不是基于 0 的索引）的形式给出。 可以有多个给定类型的查询。

**示例**：

```
Input  : arr[] = {2, 8, 6, 9, 8, 6, 8, 2, 11};
         left = 2, right = 8, element = 8
         left = 2, right = 5, element = 6      
Output : 3
         1
The element 8 appears 3 times in arr[left-1..right-1]
The element 6 appears 1 time in arr[left-1..right-1]

```

**朴素的方法**：是从左到右遍历并在找到元素时更新计数变量。

以下是朴素方法的代码：-

## C++ 

```cpp

// C++ program to find total count of an element 
// in a range 
#include<bits/stdc++.h> 
using namespace std; 

// Returns count of element in arr[left-1..right-1] 
int findFrequency(int arr[], int n, int left, 
                         int right, int element) 
{ 
    int count = 0; 
    for (int i=left-1; i<=right; ++i) 
        if (arr[i] == element) 
            ++count; 
    return count; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = {2, 8, 6, 9, 8, 6, 8, 2, 11}; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    // Print frequency of 2 from position 1 to 6 
    cout << "Frequency of 2 from 1 to 6 = "
         << findFrequency(arr, n, 1, 6, 2) << endl; 

    // Print frequency of 8 from position 4 to 9 
    cout << "Frequency of 8 from 4 to 9 = "
         << findFrequency(arr, n, 4, 9, 8); 

    return 0; 
} 

```