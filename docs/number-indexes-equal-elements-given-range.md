# 给定范围内具有相等元素的索引数

> 原文： [https://www.geeksforgeeks.org/number-indexes-equal-elements-given-range/](https://www.geeksforgeeks.org/number-indexes-equal-elements-given-range/)

给定`N`个数字和`Q`个查询，每个查询都由`L`和`R`组成，任务是找到这样的整数`i`（`L <= i < R`）的数量，以使`A[i] = A[i+1]`。 考虑基于 0 的索引。

**示例**：

```
Input : A = [1, 2, 2, 2, 3, 3, 4, 4, 4] 
        Q = 2 
        L = 1 R = 8 
        L = 0 R = 4 
Output : 5 
         2
Explanation: We have 5 index i which has 
Ai=Ai+1 in range [1, 8). We have 
2 indexes i which have Ai=Ai+1
in range [0, 4). 

Input :A = [3, 3, 4, 4] 
       Q = 2
       L = 0 R = 3
       L = 2 R = 3 
Output : 2 
         1

```



**朴素的方法**是从`L`遍历到`R`（不包括`R`）并分别针对每个查询，计算满足条件`A[i] = A[i+1]`的索引`i`的数量。

以下是朴素方法的实现：

## C++ 

```cpp

// CPP program to count the number of indexes 
// in range L R such that Ai = Ai+1 
#include <bits/stdc++.h> 
using namespace std; 

// function that answers every query in O(r-l) 
int answer_query(int a[], int n, int l, int r) 
{ 
    // traverse from l to r and count 
    // the required indexes 
    int count = 0; 
    for (int i = l; i < r; i++) 
        if (a[i] == a[i + 1]) 
            count += 1; 

    return count; 
} 

// Driver Code 
int main() 
{ 
    int a[] = { 1, 2, 2, 2, 3, 3, 4, 4, 4 }; 
    int n = sizeof(a) / sizeof(a[0]); 

    // 1-st query 
    int L, R; 
    L = 1; 
    R = 8; 

    cout << answer_query(a, n, L, R) << endl; 

    // 2nd query 
    L = 0; 
    R = 4; 
    cout << answer_query(a, n, L, R) << endl; 
    return 0; 
} 

```