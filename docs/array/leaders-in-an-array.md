# 领导者数组

> 原文： [https://www.geeksforgeeks.org/leaders-in-an-array/](https://www.geeksforgeeks.org/leaders-in-an-array/)

编写程序以打印数组中的所有领导者。 如果一个元素大于其右侧的所有元素，则为领导者。 最右边的元素始终是领导者。 例如，在数组`{16, 17, 4, 4, 3, 5, 2}`中，前导是 17、5 和 2。

令输入数组为`arr[]`，数组的大小为`size`。



**方法 1（简单）**：

使用两个循环。 外循环从 0 到大小 -1，然后从左到右依次选择所有元素。 内部循环将拾取的元素与其右侧的所有元素进行比较。 如果拾取的元素大于其右侧的所有元素，则拾取的元素为前导。

## C++ 

```cpp

#include<iostream> 
using namespace std; 

/*C++ Function to print leaders in an array */
void printLeaders(int arr[], int size) 
{ 
    for (int i = 0; i < size; i++) 
    { 
        int j; 
        for (j = i+1; j < size; j++) 
        { 
            if (arr[i] <= arr[j]) 
                break; 
        }     
        if (j == size) // the loop didn't break 
            cout << arr[i] << " "; 
  } 
} 

/* Driver program to test above function */
int main() 
{ 
    int arr[] = {16, 17, 4, 3, 5, 2}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    printLeaders(arr, n); 
    return 0; 
} 

```