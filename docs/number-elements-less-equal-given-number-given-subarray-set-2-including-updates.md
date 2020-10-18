# 给定子数组中小于或等于给定数字的元素数 | 系列 2（包括更新）

> 原文： [https://www.geeksforgeeks.org/number-elements-less-equal-given-number-given-subarray-set-2-including-updates/](https://www.geeksforgeeks.org/number-elements-less-equal-given-number-given-subarray-set-2-including-updates/)

给定数组`a[]`和查询数量`q`，将有两种查询类型：

1.  查询 0 - `update(i, v)`：两个整数`i`和`v`，表示设置`a[i] = v`。

2.  查询 1 - `count(l, r, k)`：我们需要在子数组`l`至`r`中打印小于等于`k`的整数。

给定`a[i]`，`v < = 10000`。

**示例**：

```
Input : arr[] = {5, 1, 2, 3, 4}
        q = 6
        1 1 3 1  // First value 1 means type of query is count()
        0 3 10   // First value 0 means type of query is update()
        1 3 3 4
        0 2 1
        0 0 2
        1 0 4 5
Output :
1
0
4
For first query number of values less than equal to 1 in 
arr[1..3] is 1(1 only), update a[3] = 10
There is no value less than equal to 4 in the a[3..3]
and similarly other queries are answered       

```



我们在下面的文章中讨论了仅处理`count()`查询的解决方案。 [在给定子数组中](https://www.geeksforgeeks.org/number-elements-less-equal-given-number-given-subarray/)小于或等于给定数目的元素数。

这里`update()`查询也需要处理。

**朴素方法**朴素方法是只要有更新操作就更新数组，并且只要有类型 2 查询就遍历子数组并计算有效元素。

**有效方法**：

这个想法是使用[平方根分解](https://www.geeksforgeeks.org/sqrt-square-root-decomposition-technique-set-1-introduction/)

1.  **步骤 1**：将数组划分为`sqrt(n)`个相等大小的块。 对于每个块，保持二叉索引树的大小等于该块中元素数组中最大可能元素的 1。

2.  步骤 2：对于数组中的每个元素，找出其所属的块，并使用`arr[i]`处的值 1 更新该块的位数组。

3.  步骤 3：每当有更新查询时，将对应块的位数组更新为该索引处数组的原始值，其值等于 -1，并将同一块的位数组更新为值 1 的新值。 该索引处数组的大小。

4.  步骤 4：对于类型 2 查询，您可以对范围中的每个完整块对位进行单个查询（以计数小于或等于`k`的元素），最后对于两个部分块，只需遍历这些元素 。

## C++ 

```cpp

// Number of elements less than or equal to a given 
// number in a given subarray and allowing update 
// operations. 
#include<bits/stdc++.h> 
using namespace std; 

const int MAX = 10001; 

// updating the bit array of a valid block 
void update(int idx, int blk, int val, int bit[][MAX]) 
{ 
    for (; idx<MAX; idx += (idx&-idx)) 
        bit[blk][idx] += val; 
} 

// answering the query 
int query(int l, int r, int k, int arr[], int blk_sz, 
                                      int bit[][MAX]) 
{ 
    // traversing the first block in range 
    int sum = 0; 
    while (l<r && l%blk_sz!=0 && l!=0) 
    { 
        if (arr[l] <= k) 
            sum++; 
        l++; 
    } 

    // Traversing completely overlapped blocks in 
    // range for such blocks bit array of that block 
    // is queried 
    while (l + blk_sz <= r) 
    { 
        int idx = k; 
        for (; idx > 0 ; idx -= idx&-idx) 
            sum += bit[l/blk_sz][idx]; 
        l += blk_sz; 
    } 

    // Traversing the last block 
    while (l <= r) 
    { 
        if (arr[l] <= k) 
            sum++; 
        l++; 
    } 
    return sum; 
} 

// Preprocessing the array 
void preprocess(int arr[], int blk_sz, int n, int bit[][MAX]) 
{ 
    for (int i=0; i<n; i++) 
        update(arr[i], i/blk_sz, 1, bit); 
} 

void preprocessUpdate(int i, int v, int blk_sz, 
                      int arr[], int bit[][MAX]) 
{ 
    // updating the bit array at the original 
    // and new value of array 
    update(arr[i], i/blk_sz, -1, bit); 
    update(v, i/blk_sz, 1, bit); 
    arr[i] = v; 
} 

// driver function 
int main() 
{ 
    int arr[] = {5, 1, 2, 3, 4}; 
    int n = sizeof(arr)/sizeof(arr[0]); 

    // size of block size will be equal to square root of n 
    int blk_sz = sqrt(n); 

    // initialising bit array of each block 
    // as elements of array cannot exceed 10^4 so size 
    // of bit array is accordingly 
    int bit[blk_sz+1][MAX]; 
    memset(bit, 0, sizeof(bit)); 

    preprocess(arr, blk_sz, n, bit); 
    cout << query  (1, 3, 1, arr, blk_sz, bit) << endl; 

    preprocessUpdate(3, 10, blk_sz, arr, bit); 
    cout << query(3, 3, 4, arr, blk_sz, bit) << endl; 
    preprocessUpdate(2, 1, blk_sz, arr, bit); 
    preprocessUpdate(0, 2, blk_sz, arr, bit); 
    cout << query (0, 4, 5, arr, blk_sz, bit) << endl; 
    return 0; 
} 

```

## Java

```java

// Number of elements less than or equal to a given 
// number in a given subarray and allowing update 
// operations. 

class Test 
{ 
    static final int MAX = 10001; 

    // updating the bit array of a valid block 
    static void update(int idx, int blk, int val, int bit[][]) 
    { 
        for (; idx<MAX; idx += (idx&-idx)) 
            bit[blk][idx] += val; 
    } 

    // answering the query 
    static int query(int l, int r, int k, int arr[], int blk_sz, 
                                          int bit[][]) 
    { 
        // traversing the first block in range 
        int sum = 0; 
        while (l<r && l%blk_sz!=0 && l!=0) 
        { 
            if (arr[l] <= k) 
                sum++; 
            l++; 
        } 

        // Traversing completely overlapped blocks in 
        // range for such blocks bit array of that block 
        // is queried 
        while (l + blk_sz <= r) 
        { 
            int idx = k; 
            for (; idx > 0 ; idx -= idx&-idx) 
                sum += bit[l/blk_sz][idx]; 
            l += blk_sz; 
        } 

        // Traversing the last block 
        while (l <= r) 
        { 
            if (arr[l] <= k) 
                sum++; 
            l++; 
        } 
        return sum; 
    } 

    // Preprocessing the array 
    static void preprocess(int arr[], int blk_sz, int n, int bit[][]) 
    { 
        for (int i=0; i<n; i++) 
            update(arr[i], i/blk_sz, 1, bit); 
    } 

    static void preprocessUpdate(int i, int v, int blk_sz, 
                          int arr[], int bit[][]) 
    { 
        // updating the bit array at the original 
        // and new value of array 
        update(arr[i], i/blk_sz, -1, bit); 
        update(v, i/blk_sz, 1, bit); 
        arr[i] = v; 
    } 

    // Driver method 
    public static void main(String args[]) 
    { 
        int arr[] = {5, 1, 2, 3, 4}; 

        // size of block size will be equal to square root of n 
        int blk_sz = (int) Math.sqrt(arr.length); 

        // initialising bit array of each block 
        // as elements of array cannot exceed 10^4 so size 
        // of bit array is accordingly 
        int bit[][] = new int[blk_sz+1][MAX]; 

        preprocess(arr, blk_sz, arr.length, bit); 
        System.out.println(query(1, 3, 1, arr, blk_sz, bit)); 

        preprocessUpdate(3, 10, blk_sz, arr, bit); 
        System.out.println(query(3, 3, 4, arr, blk_sz, bit)); 
        preprocessUpdate(2, 1, blk_sz, arr, bit); 
        preprocessUpdate(0, 2, blk_sz, arr, bit); 
        System.out.println(query (0, 4, 5, arr, blk_sz, bit)); 
    } 
} 

```

## Python3

```py

# Number of elements less than or equal to a given 
# number in a given subarray and allowing update 
# operations. 
MAX = 10001

# updating the bit array of a valid block 
def update(idx, blk, val, bit): 
    while idx < MAX: 
        bit[blk][idx] += val 

        idx += (idx & -idx) 

# answering the query 
def query(l, r, k, arr, blk_sz, bit): 

    # traversing the first block in range 
    summ = 0
    while l < r and l % blk_sz != 0 and l != 0: 
        if arr[l] <= k: 
            summ += 1
        l += 1

    # Traversing completely overlapped blocks in 
    # range for such blocks bit array of that block 
    # is queried 
    while l + blk_sz <= r: 
        idx = k 
        while idx > 0: 
            summ += bit[l // blk_sz][idx] 
            idx -= (idx & -idx) 

        l += blk_sz 

    # Traversing the last block 
    while l <= r: 
        if arr[l] <= k: 
            summ += 1
        l += 1

    return summ 

# Preprocessing the array 
def preprocess(arr, blk_sz, n, bit): 
    for i in range(n): 
        update(arr[i], i // blk_sz, 1, bit) 

def preprocessUpdate(i, v, blk_sz, arr, bit): 

    # updating the bit array at the original 
    # and new value of array 
    update(arr[i], i // blk_sz, -1, bit) 
    update(v, i // blk_sz, 1, bit) 
    arr[i] = v 

# Driver Code 
if __name__ == "__main__": 
    arr = [5, 1, 2, 3, 4] 
    n = len(arr) 

    # size of block size will be equal  
    # to square root of n 
    from math import sqrt 
    blk_sz = int(sqrt(n)) 

    # initialising bit array of each block 
    # as elements of array cannot exceed 10^4  
    # so size of bit array is accordingly 
    bit = [[0 for i in range(MAX)]  
              for j in range(blk_sz + 1)] 

    preprocess(arr, blk_sz, n, bit) 
    print(query(1, 3, 1, arr, blk_sz, bit)) 

    preprocessUpdate(3, 10, blk_sz, arr, bit) 
    print(query(3, 3, 4, arr, blk_sz, bit)) 
    preprocessUpdate(2, 1, blk_sz, arr, bit) 
    preprocessUpdate(0, 2, blk_sz, arr, bit) 
    print(query(0, 4, 5, arr, blk_sz, bit)) 

# This code is contributed by 
# sanjeev2552 

```

## C# 

```cs

// Number of elements less than or equal 
// to a given number in a given subarray 
// and allowing update operations. 
using System; 

class GFG  
{ 
    static int MAX = 10001; 

    // updating the bit array of a valid block 
    static void update(int idx, int blk,  
                    int val, int [,]bit) 
    { 
        for (; idx < MAX; idx += (idx&-idx)) 
            bit[blk, idx] += val; 
    } 

    // answering the query 
    static int query(int l, int r, int k, int []arr, 
                             int blk_sz, int [,]bit) 
    { 
        // traversing the first block in range 
        int sum = 0; 
        while (l < r && l % blk_sz != 0 && l != 0) 
        { 
            if (arr[l] <= k) 
                sum++; 
            l++; 
        } 

        // Traversing completely overlapped blocks in 
        // range for such blocks bit array of that block 
        // is queried 
        while (l + blk_sz <= r) 
        { 
            int idx = k; 
            for (; idx > 0 ; idx -= idx&-idx) 
                sum += bit[l/blk_sz,idx]; 
            l += blk_sz; 
        } 

        // Traversing the last block 
        while (l <= r) 
        { 
            if (arr[l] <= k) 
                sum++; 
            l++; 
        } 
        return sum; 
    } 

    // Preprocessing the array 
    static void preprocess(int []arr, int blk_sz, 
                               int n, int [,]bit) 
    { 
        for (int i=0; i<n; i++) 
            update(arr[i], i / blk_sz, 1, bit); 
    } 

    static void preprocessUpdate(int i, int v, int blk_sz, 
                                    int []arr, int [,]bit) 
    { 
        // updating the bit array at the original 
        // and new value of array 
        update(arr[i], i/blk_sz, -1, bit); 
        update(v, i/blk_sz, 1, bit); 
        arr[i] = v; 
    } 

    // Driver method 
    public static void Main() 
    { 
        int []arr = {5, 1, 2, 3, 4}; 

        // size of block size will be  
        // equal to square root of n 
        int blk_sz = (int) Math.Sqrt(arr.Length); 

        // initialising bit array of each block 
        // as elements of array cannot exceed 10^4 so size 
        // of bit array is accordingly 
        int [,]bit = new int[blk_sz+1,MAX]; 

        preprocess(arr, blk_sz, arr.Length, bit); 
        Console.WriteLine(query(1, 3, 1, arr, blk_sz, bit)); 

        preprocessUpdate(3, 10, blk_sz, arr, bit); 
        Console.WriteLine(query(3, 3, 4, arr, blk_sz, bit)); 
        preprocessUpdate(2, 1, blk_sz, arr, bit); 
        preprocessUpdate(0, 2, blk_sz, arr, bit); 
        Console.WriteLine(query (0, 4, 5, arr, blk_sz, bit)); 
    } 
} 

// This code is contributed by Sam007 

```

**输出**：

```
1
0
4

```

问题是知道为什么没有更新操作时不使用此方法，答案在于使用此方法的空间复杂性 2 维位数组以及其大小取决于数组的最大可能值，但是当存在 没有更新操作，我们的位数组仅取决于数组的大小。

