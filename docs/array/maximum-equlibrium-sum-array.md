# 数组中的最大平衡和

> 原文： [https://www.geeksforgeeks.org/maximum-equlibrium-sum-array/](https://www.geeksforgeeks.org/maximum-equlibrium-sum-array/)

给定一个数组`arr[]`。 在`arr[]`中找到前缀和的最大值，它也是索引`i`的后缀和。

**示例**：

```
Input : arr[] = {-1, 2, 3, 0, 3, 2, -1}
Output : 4
Prefix sum of arr[0..3] = 
            Suffix sum of arr[3..6]

Input : arr[] = {-2, 5, 3, 1, 2, 6, -4, 2}
Output : 7
Prefix sum of arr[0..3] = 
              Suffix sum of arr[3..7]

```



**简单解决方案**一步一步地检查每个元素的给定条件（前缀和等于后缀和），然后返回满足给定条件的元素的最大值。

## C++ 

```cpp

// CPP program to find  
// maximum equilibrium sum. 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find  
// maximum equilibrium sum. 
int findMaxSum(int arr[], int n) 
{ 
    int res = INT_MIN; 
    for (int i = 0; i < n; i++) 
    { 
    int prefix_sum = arr[i]; 
    for (int j = 0; j < i; j++) 
        prefix_sum += arr[j]; 

    int suffix_sum = arr[i]; 
    for (int j = n - 1; j > i; j--) 
        suffix_sum += arr[j]; 

    if (prefix_sum == suffix_sum) 
        res = max(res, prefix_sum); 
    } 
    return res; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = {-2, 5, 3, 1,  
                  2, 6, -4, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << findMaxSum(arr, n); 
    return 0; 
} 

```