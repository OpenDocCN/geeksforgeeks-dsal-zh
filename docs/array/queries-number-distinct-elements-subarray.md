# 查询子数组中不同元素的数量

> 原文： [https://www.geeksforgeeks.org/queries-number-distinct-elements-subarray/](https://www.geeksforgeeks.org/queries-number-distinct-elements-subarray/)

给定大小为`n`且查询数量为`q`的数组`a[]`。 每个查询可以用两个整数`l`和`r`表示。 您的任务是在子数组`l`至`r`中打印不同整数的数量。假设`a [i] <= 10^6`。

**示例**：

```
Input : a[] = {1, 1, 2, 1, 3}
        q = 3
        0 4
        1 3
        2 4
Output :3
        2
        3
In query 1, number of distinct integers
in a[0...4] is 3 (1, 2, 3)
In query 2, number of distinct integers 
in a[1..3] is 2 (1, 2)
In query 3, number of distinct integers 
in a[2..4] is 3 (1, 2, 3)

```



这个想法是使用[二叉索引树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)

1.  **步骤 1**：取大小为`10 ^ 6`的数组`last_visit`，其中`last_visit[i]`持有数组`a`中数字`i`的最右边索引。 将此数组初始化为 -1。

2.  **步骤 2**：按右端`r`的升序对所有查询进行排序。

3.  **步骤 3**：在数组`BIT[]`中创建[二叉索引树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)。 开始遍历数组`a`并同时查询，并检查`last_visit[a[i]]`是否为 -1。 如果不是，请在`last_visit[a[i]]`处使用值 -1 更新位数组。

4.  **步骤 4**：设置`last_visit[a[i]] = i`，并在索引`i`处将位数组更新为值 1 。

5.  **步骤 5**：通过查询位数组来回答`r`等于`i`的所有查询。 在对查询进行排序时，可以很容易地做到这一点。

## C++ 

```cpp

// C++ code to find number of distinct numbers 
// in a subarray 
#include<bits/stdc++.h> 
using namespace std; 

const int MAX = 1000001; 

// structure to store queries 
struct Query 
{ 
    int l, r, idx; 
}; 

// cmp function to sort queries according to r 
bool cmp(Query x, Query y) 
{ 
    return x.r < y.r; 
} 

// updating the bit array 
void update(int idx, int val, int bit[], int n) 
{ 
    for (; idx <= n; idx += idx&-idx) 
        bit[idx] += val; 
} 

// querying the bit array 
int query(int idx, int bit[], int n) 
{ 
    int sum = 0; 
    for (; idx>0; idx-=idx&-idx) 
        sum += bit[idx]; 
    return sum; 
} 

void answeringQueries(int arr[], int n, Query queries[], int q) 
{ 
    // initialising bit array 
    int bit[n+1]; 
    memset(bit, 0, sizeof(bit)); 

    // holds the rightmost index of any number 
    // as numbers of a[i] are less than or equal to 10^6 
    int last_visit[MAX]; 
    memset(last_visit, -1, sizeof(last_visit)); 

    // answer for each query 
    int ans[q]; 
    int query_counter = 0; 
    for (int i=0; i<n; i++) 
    { 
        // If last visit is not -1 update -1 at the 
        // idx equal to last_visit[arr[i]] 
        if (last_visit[arr[i]] !=-1) 
            update (last_visit[arr[i]] + 1, -1, bit, n); 

        // Setting last_visit[arr[i]] as i and updating 
        // the bit array accordingly 
        last_visit[arr[i]] = i; 
        update(i + 1, 1, bit, n); 

        // If i is equal to r of any query  store answer 
        // for that query in ans[] 
        while (query_counter < q && queries[query_counter].r == i) 
        { 
            ans[queries[query_counter].idx] = 
                     query(queries[query_counter].r + 1, bit, n)- 
                     query(queries[query_counter].l, bit, n); 
            query_counter++; 
        } 
    } 

    // print answer for each query 
    for (int i=0; i<q; i++) 
        cout << ans[i] << endl; 
} 

// driver code 
int main() 
{ 
    int a[] = {1, 1, 2, 1, 3}; 
    int n = sizeof(a)/sizeof(a[0]); 
    Query queries[3]; 
    queries[0].l = 0; 
    queries[0].r = 4; 
    queries[0].idx = 0; 
    queries[1].l = 1; 
    queries[1].r = 3; 
    queries[1].idx = 1; 
    queries[2].l = 2; 
    queries[2].r = 4; 
    queries[2].idx = 2; 
    int q = sizeof(queries)/sizeof(queries[0]); 
    sort(queries, queries+q, cmp); 
    answeringQueries(a, n, queries, q); 
    return 0; 
} 

```

## Java

```java

// Java code to find number of distinct numbers  
// in a subarray  
import java.io.*; 
import java.util.*; 

class GFG  
{ 
    static int MAX = 1000001; 

    // structure to store queries 
    static class Query  
    { 
        int l, r, idx; 
    } 

    // updating the bit array 
    static void update(int idx, int val,  
                        int bit[], int n)  
    { 
        for (; idx <= n; idx += idx & -idx) 
            bit[idx] += val; 
    } 

    // querying the bit array 
    static int query(int idx, int bit[], int n)  
    { 
        int sum = 0; 
        for (; idx > 0; idx -= idx & -idx) 
            sum += bit[idx]; 
        return sum; 
    } 

    static void answeringQueries(int[] arr, int n,  
                                Query[] queries, int q) 
    { 

        // initialising bit array 
        int[] bit = new int[n + 1]; 
        Arrays.fill(bit, 0); 

        // holds the rightmost index of any number 
        // as numbers of a[i] are less than or equal to 10^6 
        int[] last_visit = new int[MAX]; 
        Arrays.fill(last_visit, -1); 

        // answer for each query 
        int[] ans = new int[q]; 
        int query_counter = 0; 
        for (int i = 0; i < n; i++)  
        { 

            // If last visit is not -1 update -1 at the 
            // idx equal to last_visit[arr[i]] 
            if (last_visit[arr[i]] != -1) 
                update(last_visit[arr[i]] + 1, -1, bit, n); 

            // Setting last_visit[arr[i]] as i and updating 
            // the bit array accordingly 
            last_visit[arr[i]] = i; 
            update(i + 1, 1, bit, n); 

            // If i is equal to r of any query store answer 
            // for that query in ans[] 
            while (query_counter < q && queries[query_counter].r == i)  
            { 
                ans[queries[query_counter].idx] =  
                        query(queries[query_counter].r + 1, bit, n) 
                        - query(queries[query_counter].l, bit, n); 
                query_counter++; 
            } 
        } 

        // print answer for each query 
        for (int i = 0; i < q; i++) 
            System.out.println(ans[i]); 
    } 

    // Driver Code 
    public static void main(String[] args)  
    { 
        int a[] = { 1, 1, 2, 1, 3 }; 
        int n = a.length; 
        Query[] queries = new Query[3]; 
        for (int i = 0; i < 3; i++) 
            queries[i] = new Query(); 
        queries[0].l = 0; 
        queries[0].r = 4; 
        queries[0].idx = 0; 
        queries[1].l = 1; 
        queries[1].r = 3; 
        queries[1].idx = 1; 
        queries[2].l = 2; 
        queries[2].r = 4; 
        queries[2].idx = 2; 
        int q = queries.length; 
        Arrays.sort(queries, new Comparator<Query>()  
        { 
            public int compare(Query x, Query y) 
            { 
                if (x.r < y.r) 
                    return -1; 
                else if (x.r == y.r) 
                    return 0; 
                else
                    return 1; 
            } 
        }); 
        answeringQueries(a, n, queries, q); 
    } 
} 

// This code is contributed by 
// sanjeev2552 

```

## Python3

```py

# Python3 code to find number of  
# distinct numbers in a subarray 
MAX = 1000001

# structure to store queries 
class Query: 
    def __init__(self, l, r, idx): 
        self.l = l 
        self.r = r 
        self.idx = idx 

# updating the bit array 
def update(idx, val, bit, n): 
    while idx <= n: 
        bit[idx] += val 
        idx += idx & -idx 

# querying the bit array 
def query(idx, bit, n): 
    summ = 0
    while idx: 
        summ += bit[idx] 
        idx -= idx & -idx 
    return summ 

def answeringQueries(arr, n, queries, q): 

    # initialising bit array 
    bit = [0] * (n + 1) 

    # holds the rightmost index of  
    # any number as numbers of a[i] 
    # are less than or equal to 10^6 
    last_visit = [-1] * MAX

    # answer for each query 
    ans = [0] * q 

    query_counter = 0
    for i in range(n): 

        # If last visit is not -1 update -1 at the 
        # idx equal to last_visit[arr[i]] 
        if last_visit[arr[i]] != -1: 
            update(last_visit[arr[i]] + 1, -1, bit, n) 

        # Setting last_visit[arr[i]] as i and  
        # updating the bit array accordingly 
        last_visit[arr[i]] = i 
        update(i + 1, 1, bit, n) 

        # If i is equal to r of any query store answer 
        # for that query in ans[] 
        while query_counter < q and queries[query_counter].r == i: 
            ans[queries[query_counter].idx] = \ 
                        query(queries[query_counter].r + 1, bit, n) - \ 
                        query(queries[query_counter].l, bit, n) 
            query_counter += 1

    # print answer for each query 
    for i in range(q): 
        print(ans[i]) 

# Driver Code 
if __name__ == "__main__": 
    a = [1, 1, 2, 1, 3] 
    n = len(a) 
    queries = [Query(0, 4, 0),  
               Query(1, 3, 1),  
               Query(2, 4, 2)] 
    q = len(queries) 

    queries.sort(key = lambda x: x.r) 
    answeringQueries(a, n, queries, q) 

# This code is contributed by 
# sanjeev2552 

```

**输出**：

```
3
2
3

```

