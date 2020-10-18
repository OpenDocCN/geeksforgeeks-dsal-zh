# 计算最小步数以获得给定的所需数组

> 原文： [https://www.geeksforgeeks.org/count-minimum-steps-get-given-desired-array/](https://www.geeksforgeeks.org/count-minimum-steps-get-given-desired-array/)

考虑一个具有`n`个元素的数组，所有元素的值为零。 我们可以在数组上执行以下操作。

1.  增量操作：从数组中选择 1 个元素，并将其值增加 1。

2.  加倍运算：将数组所有元素的值加倍。

**我们得到了包含`n`个元素的所需数组`target[]`。 计算并返回将数组从全零更改为所需数组所需的最小数量的操作。**

**示例**：

```
Input: target[] = {2, 3}
Output: 4
To get the target array from {0, 0}, we 
first increment both elements by 1 (2 
operations), then double the array (1 
operation). Finally increment second
element (1 more operation)

Input: target[] = {2, 1}
Output: 3
One of the optimal solution is to apply the 
incremental operation 2 times to first and 
once on second element.

Input: target[] = {16, 16, 16}
Output: 7
The output solution looks as follows. First 
apply an incremental operation to each element. 
Then apply the doubling operation four times. 
Total number of operations is 3+4 = 7
```



需要注意的重要一件事是任务是计算获得给定目标数组的步骤数（而不是将零数组转换为目标数组）。

想法是遵循相反的步骤，即将目标转换为零数组。 以下是步骤。

```
Take the target array first. 

Initialize result as 0\. 

If all are even, divide all elements by 2 
and increment result by 1\. 

Find all odd elements, make them even by 
reducing them by 1\. and for every reduction,
increment result by 1.

Finally, we get all zeros in target array.
```

下面是上述算法的实现。

## C++ 

```cpp

/* C++ program to count minimum number of operations 
   to get the given target array */
#include <bits/stdc++.h> 
using namespace std; 

// Returns count of minimum operations to convert a 
// zero array to target array with increment and 
// doubling operations. 
// This function computes count by doing reverse 
// steps, i.e., convert target to zero array. 
int countMinOperations(unsigned int target[], int n) 
{ 
    // Initialize result (Count of minimum moves) 
    int result = 0; 

    // Keep looping while all elements of target 
    // don't become 0\. 
    while (1) 
    { 
        // To store count of zeroes in current 
        // target array 
        int zero_count = 0; 

        int i;  // To find first odd element 
        for (i=0; i<n; i++) 
        { 
            // If odd number found 
            if (target[i] & 1) 
                break; 

            // If 0, then increment zero_count 
            else if (target[i] == 0) 
                zero_count++; 
        } 

        // All numbers are 0 
        if (zero_count == n) 
          return result; 

        // All numbers are even 
        if (i == n) 
        { 
            // Divide the whole array by 2 
            // and increment result 
            for (int j=0; j<n; j++) 
               target[j] = target[j]/2; 
            result++; 
        } 

        // Make all odd numbers even by subtracting 
        // one and increment result. 
        for (int j=i; j<n; j++) 
        { 
           if (target[j] & 1) 
           { 
              target[j]--; 
              result++; 
           } 
        } 
    } 
} 

/* Driver program to test above functions*/
int main() 
{ 
    unsigned int arr[] = {16, 16, 16}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << "Minimum number of steps required to "
           "get the given target array is " 
         << countMinOperations(arr, n); 
    return 0; 
} 

```