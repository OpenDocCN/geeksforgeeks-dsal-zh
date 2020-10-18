# 排序数组所需的最小交换次数

> 原文： [https://www.geeksforgeeks.org/minimum-number-swaps-required-sort-array/](https://www.geeksforgeeks.org/minimum-number-swaps-required-sort-array/)

给定 **n** 个不同元素的数组，请找到对数组进行排序所需的最小交换次数。

**示例**：

```
Input : {4, 3, 2, 1}
Output : 2
Explanation : Swap index 0 with 3 and 1 with 2 to 
              form the sorted array {1, 2, 3, 4}.

Input : {1, 5, 4, 3, 2}
Output : 2

```



通过将问题可视化为图形，可以轻松完成此操作。 如果第`i`个索引的元素必须存在于第`j`个索引中，则我们将有`n`个节点和一条从节点`i`指向节点`j`的边。 排序后的数组。

```

Graph for {4, 3, 2, 1}

```

该图现在将包含许多不相交的循环。 现在，具有 2 个节点的循环只需要进行 1 次交换即可达到正确的顺序，类似地，具有 3 个节点的循环也只需进行 2 次交换即可。

```

Graph for {4, 5, 2, 1, 5}

```

因此，

```
ans = Σ(cycle_size – 1), i = 1 ~ k
```

其中`k`是周期数。

以下是该想法的实现。

## C++ 

```cpp

// C++ program to find  minimum number of swaps 
// required to sort an array 
#include<bits/stdc++.h> 

using namespace std; 

// Function returns the minimum number of swaps 
// required to sort the array 
int minSwaps(int arr[], int n) 
{ 
    // Create an array of pairs where first 
    // element is array element and second element 
    // is position of first element 
    pair<int, int> arrPos[n]; 
    for (int i = 0; i < n; i++) 
    { 
        arrPos[i].first = arr[i]; 
        arrPos[i].second = i; 
    } 

    // Sort the array by array element values to 
    // get right position of every element as second 
    // element of pair. 
    sort(arrPos, arrPos + n); 

    // To keep track of visited elements. Initialize 
    // all elements as not visited or false. 
    vector<bool> vis(n, false); 

    // Initialize result 
    int ans = 0; 

    // Traverse array elements 
    for (int i = 0; i < n; i++) 
    { 
        // already swapped and corrected or 
        // already present at correct pos 
        if (vis[i] || arrPos[i].second == i) 
            continue; 

        // find out the number of  node in 
        // this cycle and add in ans 
        int cycle_size = 0; 
        int j = i; 
        while (!vis[j]) 
        { 
            vis[j] = 1; 

            // move to next node 
            j = arrPos[j].second; 
            cycle_size++; 
        } 

        // Update answer by adding current cycle.  
        if (cycle_size > 0) 
        { 
            ans += (cycle_size - 1); 
        } 
    } 

    // Return result 
    return ans; 
} 

// Driver program to test the above function 
int main() 
{ 
    int arr[] = {1, 5, 4, 3, 2}; 
    int n = (sizeof(arr) / sizeof(int)); 
    cout << minSwaps(arr, n); 
    return 0; 
} 

```