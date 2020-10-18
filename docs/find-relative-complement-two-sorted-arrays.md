# 查找两个排序数组的相对补码

> 原文： [https://www.geeksforgeeks.org/find-relative-complement-two-sorted-arrays/](https://www.geeksforgeeks.org/find-relative-complement-two-sorted-arrays/)

给定两个大小分别为`m`和`n`的排序数组`arr1`和`arr2`。 我们需要找到两个数组的相对补码，即`arr1 – arr2`，这意味着我们需要找到`arr1`中存在但`arr2`中不存在的所有元素。

例子：

```
Input : arr1[] = {3, 6, 10, 12, 15}
        arr2[] = {1, 3, 5, 10, 16}
Output : 6 12 15
The elements 6, 12 and 15 are present
in arr[], but not present in arr2[]

Input : arr1[] = {10, 20, 36, 59}
        arr2[] = {5, 10, 15, 59}
Output : 20 36

```



1.  取两个指针`i`和`j`分别穿过`arr1`和`arr2`。

2.  如果`arr1[i]`元素小于`arr2[j]`元素，则打印此元素并增加`i`。

3.  如果`arr1`元素大于`arr2[j]`元素，则递增`j`。

4.  否则增加`i`和`j`。

## C++ 

```cpp

// CPP program to find all those  
// elements of arr1[] that are not 
// present in arr2[] 
#include <iostream> 
using namespace std; 

void relativeComplement(int arr1[], int arr2[], 
                               int n, int m) { 

  int i = 0, j = 0; 
  while (i < n && j < m) { 

    // If current element in arr2[] is 
    // greater, then arr1[i] can't be  
    // present in arr2[j..m-1] 
    if (arr1[i] < arr2[j]) { 
      cout << arr1[i] << " "; 
      i++; 

    // Skipping smaller elements of 
    // arr2[] 
    } else if (arr1[i] > arr2[j]) { 
      j++; 

    // Equal elements found (skipping 
    // in both arrays) 
    } else if (arr1[i] == arr2[j]) { 
      i++; 
      j++; 
    } 
  } 

  // Printing remaining elements of 
  // arr1[] 
  while (i < n)  
    cout << arr1[i] << " ";   
} 

// Driver code 
int main() { 
  int arr1[] = {3, 6, 10, 12, 15}; 
  int arr2[] = {1, 3, 5, 10, 16}; 
  int n = sizeof(arr1) / sizeof(arr1[0]); 
  int m = sizeof(arr2) / sizeof(arr2[0]); 
  relativeComplement(arr1, arr2, n, m); 
  return 0; 
} 

```