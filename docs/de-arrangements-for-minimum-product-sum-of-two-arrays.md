# 两个数组的最小乘积之和的重新排列

> 原文： [https://www.geeksforgeeks.org/de-arrangements-for-minimum-product-sum-of-two-arrays/](https://www.geeksforgeeks.org/de-arrangements-for-minimum-product-sum-of-two-arrays/)

给定两个大小为`n`的数组`A[]`和`B[]`。 我们需要首先对任何数组进行置换，以使对的乘积之和（每对 1 个元素）最小。 也就是说，所有`i`的`SUM(Ai * Bi)`最小。 与置换数组相比，我们还需要计算原始数组中存在的解排列数。

例子：

```
Input : A[] = {4, 3, 2},  
        B[] = {7, 12, 5}
Output : 3
Explanation : A[] = {4, 3, 2} and B[] = {5, 7, 12}
results in minimum product sum. B[] = {7, 12, 5} 
is 3-position different from new B[].

Input : A[] = {4, 3, 2},  
        B[] = { 1, 2, 3}
Output : 0
Explanation : A[] = {4, 3, 2} and B[] = {1, 2, 3}
results in minimum product sum. B[] = {1, 2, 3} 
is exactly same as new one.

```



从两个数组中找到最小乘积之和的想法是对两个数组中的一个以递增方式进行排序，而另一个以递减方式进行排序。 这些类型的数组将始终产生最小的对乘积之和。 对两个数组进行排序将得出对值，即`A`中的哪个元素与`B[]`中的哪个元素配对。 在那之后，计算从原始数组的重新排列。

**算法**：

1.  复制两个数组。

2.  将`copy_A[]`升序排列，将`copy_B[]`降序排列。

3.  遍历所有`Ai`，在`copy_A[]`中找到`Ai`作为`copy_A[j]`，然后检查`copy_B[j] == B[i]`。 如果不相等，则增加计数。

4.  返回计数值。 那将是我们的答案。

```

// CPP program to count de-arrangements for  
// minimum product. 
#include<bits/stdc++.h> 
using namespace std; 

// function for finding de-arrangement 
int findDearrange (int A[], int B[], int n) 
{ 
    // create copy of array 
    vector <int> copy_A (A, A+n); 
    vector <int> copy_B (B, B+n); 

    // sort array in inc & dec way 
    sort(copy_A.begin(), copy_A.end()); 
    sort(copy_B.begin(), copy_B.end(),greater<int>()); 

    // count no. of de arrangements 
    int count = 0; 
    for (int i=0; i<n;i++) 
    { 
         vector<int>::iterator itA; 

         // find position of A[i] in sorted array 
         itA = lower_bound(copy_A.begin(),  
                           copy_A.end(), A[i]); 

         // check whether B[i] is same as required or not 
         if (B[i] != copy_B[itA-copy_A.begin()]) 
              count++; 
    } 

    // return count 
    return count; 
} 

// driver function 
int main() 
{ 
    int A[] = {1, 2, 3, 4}; 
    int B[] = {6, 3, 4, 5}; 
    int n = sizeof(A) /sizeof(A[0]);; 
    cout << findDearrange(A,B,n); 
    return 0; 
}  

```

输出：

```
2

```



* * *

* * *



