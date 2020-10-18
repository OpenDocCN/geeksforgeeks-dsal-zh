# 计算总数小于给定值的三元组

> 原文： [https://www.geeksforgeeks.org/count-triplets-with-sum-smaller-that-a-given-value/](https://www.geeksforgeeks.org/count-triplets-with-sum-smaller-that-a-given-value/)

给定一个由不同整数组成的数组和一个求和值。 查找总和小于给定总和值的三元组的数量。 预期时间复杂度为 `O(n^2)`。

**示例**：

```
Input : arr[] = {-2, 0, 1, 3}
        sum = 2.
Output : 2
Explanation :  Below are triplets with sum less than 2
               (-2, 0, 1) and (-2, 0, 3) 

Input : arr[] = {5, 1, 3, 4, 7}
        sum = 12.
Output : 4
Explanation :  Below are triplets with sum less than 12
               (1, 3, 4), (1, 3, 5), (1, 3, 7) and 
               (1, 4, 5)
```



一个**简单解决方案**是运行三个循环，一个接一个地考虑所有三元组。 对于每个三元组，如果三元组的总和小于给定的总和，则比较总和和增量计数。

## C++ 

```cpp

// A Simple C++ program to count triplets with sum smaller 
// than a given value 
#include<bits/stdc++.h> 
using namespace std; 

int countTriplets(int arr[], int n, int sum) 
{ 
    // Initialize result 
    int ans = 0; 

    // Fix the first element as A[i] 
    for (int i = 0; i < n-2; i++) 
    { 
       // Fix the second element as A[j] 
       for (int j = i+1; j < n-1; j++) 
       { 
           // Now look for the third number 
           for (int k = j+1; k < n; k++) 
               if (arr[i] + arr[j] + arr[k] < sum) 
                   ans++; 
       } 
    } 

    return ans; 
} 

// Driver program 
int main() 
{ 
    int arr[] = {5, 1, 3, 4, 7}; 
    int n = sizeof arr / sizeof arr[0]; 
    int sum = 12; 
    cout << countTriplets(arr, n, sum) << endl; 
    return 0; 
} 

```