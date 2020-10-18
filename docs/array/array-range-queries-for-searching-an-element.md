# 数组范围查询以搜索元素

> 原文： [https://www.geeksforgeeks.org/array-range-queries-for-searching-an-element/](https://www.geeksforgeeks.org/array-range-queries-for-searching-an-element/)

给定一个由`N`个元素组成的数组和形式为`L R X`的`Q`个查询。对于每个查询，必须输出元素`X`是否存在于索引`L`和`R`（包括）之间的数组中。

**先决条件**： [Mo 的算法](https://www.geeksforgeeks.org/mos-algorithm-query-square-root-decomposition-set-1-introduction/)

**示例**：

```
Input : N = 5
        arr = [1, 1, 5, 4, 5]
        Q = 3
        1 3 2
        2 5 1
        3 5 5         
Output : No
         Yes
         Yes
Explanation :
For the first query, 2 does not exist between the indices 1 and 3.
For the second query, 1 exists between the indices 2 and 5.
For the third query, 5 exists between the indices 3 and 5.

```

**朴素方法**：

朴素方法是针对每个查询遍历从`L`到`R`的元素，线性搜索`X`。在最坏的情况下，从`L`到`R`可以有`N`个元素，因此 每个查询的最差情况时间复杂度为`O(n)`。 因此，对于所有`Q`查询，时间复​​杂度将变为`O(Q * N)`。

**使用联合查找方法**：

此方法仅检查所有连续相等值中的一个元素。 如果`X`不等于这些值，则算法会跳过所有其他相等的元素，并继续遍历下一个不同的元素。 该算法显然仅在连续存在大量相等元素时才有用。

**算法**：

1.  将所有连续的相等元素合并为一组。

2.  处理查询时，从`R`开始。让`index = R`。

3.  将`a[index]`与`X`进行比较。如果它们相等，则打印`"Yes"`，然后遍历其余范围。 否则，跳过所有属于`a[index]`组的连续元素。 索引等于该组的根索引的 1。

4.  继续上述步骤，直到找到`X`或直到索引小于`L`。

5.  如果索引小于`L`，则打印`"No"`。

以下是上述想法的实现。

## C++ 

```cpp

// Program to determine if the element 
// exists for different range queries 
#include <bits/stdc++.h> 
using namespace std; 

// Structure to represent a query range 
struct Query 
{ 
    int L, R, X; 
}; 

const int maxn = 100; 

int root[maxn]; 

// Find the root of the group containing 
// the element at index x 
int find(int x) 
{ 
    return x == root[x] ? x : root[x] = 
                find(root[x]); 
} 

// merge the two groups containing elements 
// at indices x and y into one group 
int uni(int x, int y) 
{ 
    int p = find(x), q = find(y); 
    if (p != q) { 
        root[p] = root[q]; 
    } 
} 

void initialize(int a[], int n, Query q[], int m) 
{ 
    // make n subsets with every 
    // element as its root 
    for (int i = 0; i < n; i++) 
        root[i] = i; 

    // consecutive elements equal in value are 
    // merged into one single group 
    for (int i = 1; i < n; i++) 
        if (a[i] == a[i - 1]) 
            uni(i, i - 1); 
} 

// Driver code 
int main() 
{ 
    int a[] = { 1, 1, 5, 4, 5 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    Query q[] = { { 0, 2, 2 }, { 1, 4, 1 }, 
                  { 2, 4, 5 } }; 
    int m = sizeof(q) / sizeof(q[0]); 
    initialize(a, n, q, m); 

    for (int i = 0; i < m; i++) 
    { 
        int flag = 0; 
        int l = q[i].L, r = q[i].R, x = q[i].X; 
        int p = r; 

        while (p >= l) 
        { 

            // check if the current element in 
            // consideration is equal to x or not 
            // if it is equal, then x exists in the range 
            if (a[p] == x) 
            { 
                flag = 1; 
                break; 
            } 
            p = find(p) - 1; 
        } 

        // Print if x exists or not 
        if (flag != 0) 
            cout << x << " exists between [" << l  
                 << ", " << r << "] " << endl; 
        else
            cout << x << " does not exist between [" 
                << l << ", " << r  << "] " << endl; 
    } 
} 

```