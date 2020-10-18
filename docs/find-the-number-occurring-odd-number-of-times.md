# 查找出现次数的奇数

> 原文： [https://www.geeksforgeeks.org/find-the-number-occurring-odd-number-of-times/](https://www.geeksforgeeks.org/find-the-number-occurring-odd-number-of-times/)

给定一个正整数数组。 除一个数字为奇数次外，所有数字均出现偶数次。 在`O(n)`时间&恒定空间中找到数字。

**示例**：

```
Input : arr = {1, 2, 3, 2, 3, 1, 3}
Output : 3

Input : arr = {5, 7, 2, 7, 5, 2, 5}
Output : 5

```



**简单解决方案**是运行两个嵌套循环。 外循环一一拾取所有元素，内循环计数外循环拾取的元素的出现次数。 该解决方案的时间复杂度为 `O(n^2)`。

以下是暴力方法的实现：

## C++ 

```cpp

// C++ program to find the element  
// occurring odd number of times 
#include<bits/stdc++.h> 
using namespace std; 

// Function to find the element  
// occurring odd number of times 
int getOddOccurrence(int arr[], int arr_size) 
{ 
    for (int i = 0; i < arr_size; i++) { 

        int count = 0; 

        for (int j = 0; j < arr_size; j++) 
        { 
            if (arr[i] == arr[j]) 
                count++; 
        } 
        if (count % 2 != 0) 
            return arr[i]; 
    } 
    return -1; 
} 

// driver code 
int main() 
    { 
        int arr[] = { 2, 3, 5, 4, 5, 2, 
                      4, 3, 5, 2, 4, 4, 2 }; 
        int n = sizeof(arr) / sizeof(arr[0]); 

        // Function calling 
        cout << getOddOccurrence(arr, n); 

        return 0; 
    } 

```