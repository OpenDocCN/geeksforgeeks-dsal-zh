# 合并两个有`O(1)`额外空间的排序数组

> 原文： [https://www.geeksforgeeks.org/merge-two-sorted-arrays-o1-extra-space/](https://www.geeksforgeeks.org/merge-two-sorted-arrays-o1-extra-space/)

我们给了两个排序数组。 我们需要合并这两个数组，以使初始编号（完成排序后）在第一个数组中，而其余的数字在第二个数组中。`O(1)`中允许有多余的空间。

例：

```
Input: ar1[] = {10};
       ar2[] = {2, 3};
Output: ar1[] = {2}
        ar2[] = {3, 10}  

Input: ar1[] = {1, 5, 9, 10, 15, 20};
       ar2[] = {2, 3, 8, 13};
Output: ar1[] = {1, 2, 3, 5, 8, 9}
        ar2[] = {10, 13, 15, 20} 

```



如果允许我们使用额外的空间，则此任务很简单，并且为`O(m + n)`。 但是，如果不允许有多余的空间，并且看起来在最坏的情况下不到`O(m * n)`，那么看起来就变得非常复杂。

这个想法是从`ar2[]`的最后一个元素开始，然后在`ar1[]`中搜索它。 如果`ar1[]`中有一个更大的元素，那么我们将`ar1[]`的最后一个元素移到`ar2[]`。 为了使`ar1[]`和`ar2[]`保持排序，我们需要将`ar2[]`的最后一个元素放置在`ar1[]`中的正确位置。 为此，我们可以使用[插入排序](http://geeksquiz.com/insertion-sort/)插入类型。 下面是算法：

```
1) Iterate through every element of ar2[] starting from last 
   element. Do following for every element ar2[i]
    a) Store last element of ar1[i]: last = ar1[i]
    b) Loop from last element of ar1[] while element ar1[j] is 
       smaller than ar2[i].
          ar1[j+1] = ar1[j] // Move element one position ahead
          j--
    c) If any element of ar1[] was moved or (j != m-1)
          ar1[j+1] = ar2[i] 
          ar2[i] = last  

```

在上面的循环中，`ar1[]`和`ar2[]`中的元素始终保持排序状态。

下面是上述算法的实现。

## C++ 

```cpp

// C++ program to merge two sorted arrays with O(1) extra space. 
#include <bits/stdc++.h> 
using namespace std; 

// Merge ar1[] and ar2[] with O(1) extra space 
void merge(int ar1[], int ar2[], int m, int n) 
{ 
    // Iterate through all elements of ar2[] starting from 
    // the last element 
    for (int i=n-1; i>=0; i--) 
    { 
        /* Find the smallest element greater than ar2[i]. Move all 
           elements one position ahead till the smallest greater 
           element is not found */
        int j, last = ar1[m-1]; 
        for (j=m-2; j >= 0 && ar1[j] > ar2[i]; j--) 
            ar1[j+1] = ar1[j]; 

        // If there was a greater element 
        if (j != m-2 || last > ar2[i]) 
        { 
            ar1[j+1] = ar2[i]; 
            ar2[i] = last; 
        } 
    } 
} 

// Driver program 
int main(void) 
{ 
    int ar1[] = {1, 5, 9, 10, 15, 20}; 
    int ar2[] = {2, 3, 8, 13}; 
    int m = sizeof(ar1)/sizeof(ar1[0]); 
    int n = sizeof(ar2)/sizeof(ar2[0]); 
    merge(ar1, ar2, m, n); 

    cout << "After Merging nFirst Array: "; 
    for (int i=0; i<m; i++) 
        cout << ar1[i] << " "; 
    cout << "nSecond Array: "; 
    for (int i=0; i<n; i++) 
        cout << ar2[i] << " "; 
   return 0; 
} 

```