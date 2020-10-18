# 计算将`L-R`范围内的所有数字相除的元素

> 原文： [https://www.geeksforgeeks.org/count-elements-which-divide-all-numbers-in-range-l-r/](https://www.geeksforgeeks.org/count-elements-which-divide-all-numbers-in-range-l-r/)

给定`N`个数字和`Q`个查询，每个查询都由`L`和`R`组成。任务是编写一个打印数字计数的程序，该程序将给定范围`L-R`中的所有数字相除。

**示例**：

```
Input : a = {3, 4, 2, 2, 4, 6} 
        Q = 2
        L = 1 R = 4  
        L = 2 R = 6

Output :  0
          2 

Explanation : The range 1-4 has {3, 4, 2, 2} 
which does not have any number that divides all the 
numbers in this range. 
The range 2-6 has {4, 2, 2, 4, 6} which has  2 numbers {2, 2} which divides 
all numbers in the given range. 

Input: a = {1, 2, 3, 5} 
       Q = 2 
       L = 1 R = 4 
       L = 2 R = 4 
Output: 1 
        0      

```

**朴素的方法**：针对每个查询从范围`L-R`进行迭代，并检查索引`i`处的给定元素是否将范围中的所有数字相除。 我们对所有元素进行计数，将所有数字相除。 在最坏情况下，每个查询的复杂度将为`O(n^2)`。

**以下是朴素方法的实现**：

## C++ 

```cpp

// CPP program to Count elements which 
// divides all numbers in range L-R 
#include <bits/stdc++.h> 
using namespace std; 

// function to count element 
// Time complexity O(n^2) worst case 
int answerQuery(int a[], int n,  
                int l, int r) 
{ 
    // answer for query 
    int count = 0; 

    // 0 based index 
    l = l - 1; 

    // iterate for all elements 
    for (int i = l; i < r; i++)  
    { 
        int element = a[i]; 
        int divisors = 0; 

        // check if the element divides 
        // all numbers in range 
        for (int j = l; j < r; j++)  
        { 
            // no of elements 
            if (a[j] % a[i] == 0) 
                divisors++; 
            else
                break; 
        } 

        // if all elements are divisible by a[i] 
        if (divisors == (r - l)) 
            count++; 
    } 

    // answer for every query 
    return count; 
} 

// Driver Code 
int main() 
{ 
    int a[] = { 1, 2, 3, 5 }; 
    int n = sizeof(a) / sizeof(a[0]); 

    int l = 1, r = 4; 
    cout << answerQuery(a, n, l, r) << endl; 

    l = 2, r = 4;     
    cout << answerQuery(a, n, l, r) << endl; 
    return 0; 
} 

```