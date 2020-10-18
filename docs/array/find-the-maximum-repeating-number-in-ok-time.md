# 在`O(n)`时间和`O(1)`多余空间中找到最大重复数

> 原文： [https://www.geeksforgeeks.org/find-the-maximum-repeating-number-in-ok-time/](https://www.geeksforgeeks.org/find-the-maximum-repeating-number-in-ok-time/)

给定大小为`n`的数组，该数组包含从 0 到`k-1`范围内的数字，其中`k`是正整数，`k <= n`。在此数组中找到最大重复数。 例如，假设`k`为 10，则给定数组为`arr[] = {1, 2, 2, 2, 0, 2, 0, 2, 3, 8, 0, 9, 2, 3}`，最大重复数将为 2。期望的时间复杂度为`O(n)`，允许的额外空间为`O(1)`。 允许对数组进行修改。



**朴素的方法**是运行两个循环，外循环一个接一个地拾取一个元素，内循环计算被拾取元素的出现次数。 最后返回具有最大计数的元素。 该方法的时间复杂度为`O(n ^ 2)`。

**更好的方法**是创建一个大小为`k`的计数数组，并将`count[]`的所有元素初始化为 0。对输入数组的所有元素以及每个元素`arr[i]`进行迭代，增加`count[arr[i]]`。 最后，迭代`count[]`并返回具有最大值的索引。 这种方法花费`O(n)`时间，但需要`O(k)`空间。

以下是`O(n)`时间和`O(1)`额外空间方法。 让我们用一个简单的例子来理解该方法，其中`arr[] = {2, 3, 3, 5, 3, 4, 1, 1, 7}`，`k = 8`，`n = 8`（`arr[]`中的元素数）。

1.  迭代输入数组`arr[]`，对于每个元素`arr[i]`，将`arr[arr[i] % k]`递增`k`（`arr []`变成`{2, 11, 11, 29, 11, 12, 1, 15}`）

2.  在修改后的数组中找到最大值（最大值为 29）。 最大值的索引是最大重复元素（索引 29 是 3）。

3.  如果我们想找回原始数组，可以再遍历该数组一次，并执行`arr[i] = arr [i] % k`其中`i`从 0 到`n-1`变化。

**以上算法如何工作？** 由于我们使用`arr[i] % k`作为索引，并在索引`arr[i] % k`处添加值`k`，因此该索引为 等于最大重复元素最后将具有最大值。 注意，`k`在等于最大重复元素的索引处被添加最大次数，并且所有数组元素都小于`k`。

以下是上述算法的 C++ 实现。

## C++ 

```cpp

// C++ program to find the maximum repeating number 

#include<iostream> 
using namespace std; 

// Returns maximum repeating element in arr[0..n-1]. 
// The array elements are in range from 0 to k-1 
int maxRepeating(int* arr, int n, int k) 
{ 
    // Iterate though input array, for every element 
    // arr[i], increment arr[arr[i]%k] by k 
    for (int i = 0; i< n; i++) 
        arr[arr[i]%k] += k; 

    // Find index of the maximum repeating element 
    int max = arr[0], result = 0; 
    for (int i = 1; i < n; i++) 
    { 
        if (arr[i] > max) 
        { 
            max = arr[i]; 
            result = i; 
        } 
    } 

    /* Uncomment this code to get the original array back 
       for (int i = 0; i< n; i++) 
          arr[i] = arr[i]%k; */

    // Return index of the maximum element 
    return result; 
} 

// Driver program to test above function 
int main() 
{ 
    int arr[] = {2, 3, 3, 5, 3, 4, 1, 7}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int k = 8; 

    cout << "The maximum repeating number is " << 
         maxRepeating(arr, n, k) << endl; 

    return 0; 
} 

```