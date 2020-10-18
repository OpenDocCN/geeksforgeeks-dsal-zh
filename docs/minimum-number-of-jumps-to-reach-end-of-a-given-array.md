# 到达终点的最小跳数

> 原文： [https://www.geeksforgeeks.org/minimum-number-of-jumps-to-reach-end-of-a-given-array/](https://www.geeksforgeeks.org/minimum-number-of-jumps-to-reach-end-of-a-given-array/)

给定一个整数数组，其中每个元素代表可以从该元素进行的最大步数。 编写一个函数以返回到达数组末尾（从第一个元素开始）的最小跳转数。 如果一个元素为 0，则不能在该元素中移动。

**示例**：

```
Input: arr[] = {1, 3, 5, 8, 9, 2, 6, 7, 6, 8, 9}
Output: 3 (1-> 3 -> 8 -> 9)
Explanation: Jump from 1st element 
to 2nd element as there is only 1 step, 
now there are three options 5, 8 or 9\. 
If 8 or 9 is chosen then the end node 9 
can be reached. So 3 jumps are made.

Input:  arr[] = {1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1}
Output: 10
Explanation: In every step a jump 
is needed so the count of jumps is 10.

```

第一个元素是 1，因此只能转到 3。第二个元素是 3，因此最多可以执行 3 个步骤，例如到 5 或 8 或 9。



 **方法 1**：朴素递归方法。

**方法**：朴素的方法是从第一个元素开始，然后递归调用从第一个元素可到达的所有元素。 可以使用从第一个可到达元素开始到达终点所需的最小跳数来计算从第一个到达终点的最小跳数。

`minJumps(start, end) = Min(minJumps(k. end))`，从开始就可以到达所有`k`。

## C++ 

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to return the minimum number 
// of jumps to reach arr[h] from arr[l] 
int minJumps(int arr[], int n) 
{ 

    // Base case: when source and 
    // destination are same 
    if (n == 1) 
        return 0; 

    // Traverse through all the points 
    // reachable from arr[l] 
    // Recursivel, get the minimum number 
    // of jumps needed to reach arr[h] from 
    // these reachable points 
    int res = INT_MAX; 
    for (int i = n - 2; i >= 0; i--) { 
        if (i + arr[i] >= n - 1) { 
            int sub_res = minJumps(arr, i + 1); 
            if (sub_res != INT_MAX) 
                res = min(res, sub_res + 1); 
        } 
    } 

    return res; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 1, 3, 6, 3, 2, 
                  3, 6, 8, 9, 5 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "Minimum number of jumps to"; 
    cout << " reach the end is " << minJumps(arr, n); 
    return 0; 
} 

// This code is contributed 
// by Shivi_Aggarwal 

```